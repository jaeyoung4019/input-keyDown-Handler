# input-keyDown-Handler

어떻게 구현하는 것이 가장 범용적이고 재사용이 많을까도 중요하지만 처음 구현해보는 것이라 우선 작동원리부터 파악하기 위해서 매개변수를 넘기는 방식으로 만들어 보았습니다.

Search Hook 에서 제공하도록 function 을 Hook 에 제작하고
```ts

    const enterKeyDown = useCallback(
            (fun: (value: any) => void) => (value: string) => {
                fun(value);
            },
            []
        );
        
```

추가 해줍니다. 이렇게 하면 매개변수로 펑션을 받아서 value 를 받는 function을 실행할 수 있습니다.

그런 뒤에 대상이 되는 Text Component 에 onKeyDown Handler 를 추가해주도록 했습니다.

기능상 Text Input 에 존재해야 맞다고 생각했기 때문입니다.

```ts
    const onKeyDownHandler = (e: React.KeyboardEvent<HTMLInputElement>) => {
        const {value}  = e.target as HTMLInputElement;
        if (e.key === "Enter") {
            if (onKeyDown) {
                onKeyDown(value)
            }
        }
    }
```

그래서 이렇게 구현한 다음 enter 를 인식해서 현재 input Tag 의 Value 를 리턴받아 사용하도록 하였습니다.

```ts

  function testEnterKey (value: any) {
      console.log("test!!!     " , value)
  }
  
```

이런 식으로 생성하고 테스트해서 enter 처리시 value 가 정상적으로 넘어오는가를 체크해보면
![image](https://github.com/jaeyoung4019/input-keyDown-Handler/assets/135151752/970f9c5d-d67d-4b9b-830d-cf3fd2a41597)


Input Component 의 onkeyDown 매개 변수는 아래처럼
```ts

    <TextInput onChange={onChangeFunction("text2")} value={value.text2} onKeyDown={enterKey(testEnterKey)} />

```
