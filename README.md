# 10월 8일자 수업

# 1. Node.js 설치

우선 Node.js를 사용하기 위해

Link: [Node.js][nodelink]

[nodelink]: https://nodejs.org/en/ "Go Node.js"

해당 링크로 이동하여 최신버전의 Node.js LTS 버전을 다운로드합니다.

이미 10버전 이상의 Node.js가 설치되어 있다면 이 부분은 생략해도 좋습니다.

설치 확인을 위해 cmd를 실행하고 __node__ 를 입력해봅니다.

자신이 설치한 Node.js의 버전이 출력되면 안정적으로 설치가 완료된 것입니다.

추가적으로 __1 + 1__ 이나 __console.log(2)__ 등을 실행해보며 오류가 없나 확인해봅니다.

# 2. 폴더 생성과 작업 환경 설정

Node.js의 환경은 웹 브라우저의 console 환경과 유사합니다.

cmd로 접속한 node 환경에서 여러 동작을 시행해 보았고 문제가 없다면 이제 작업을 할 폴더를 생성해봅시다.

폴더명은 본인이 원하는 이름으로 설정하시고 해당 폴더 안에

* Node 폴더
  * index.js
  
위와 같은 형식으로 문서를 만들어주세요.

생성한 폴더의 터미널에 express 프레임워크를 install 해야합니다.

본인 폴더 위치에서 터미널을 열어 주시고 __npm install express__ 라고 입력하여 express 프레임워크를 해당 폴더 위치에 install 해줍니다.

* Node 폴더
  * node_modules
  * package-lock.json
  
위와 같이 폴더, 파일 한개씩 생성 되었다면 install에 성공한 것입니다.

# 3. 서버 동작

우린 express 프레임워크를 통해 Node.js를 서버로써 동작시킬 수 있습니다.

index.js 파일에

```
const express = require('express')
const app = express()

app.get('/', (req, res) => {
    res.send('I am working!!')
})

app.get('/robot', (req, res) => {
    res.send('I am robot!!')
})

const port = 8000
app.listen(port, () => {
    console.log(`server is running on port: ${port}`)
})
```

해당 코드를 적어주세요.

express라는 변수에 우리가 install한 express 프레임워크에 대한 내용들을 저장합니다.

app변수에는 함수 형태로 저장된 express를 저장합니다.

app.get 부분에서 첫번째 매개변수 안에 서버로 접속할 때 어떤 통로를 거칠지 정하는 것입니다.

res는 get() 함수가 호출될 때 response를 받게될 것입니다.

이는 매개변수의 이름과는 관계가 없고 순서와 관계가 있습니다.

get() 함수에서 위 코드와 다르게 매개변수를 더 늘릴수도 더 줄일수도 있고 이러한 동작이 가능한건 오버로딩 기법 덕분입니다.

다만 보통은 위와 같은 매개변수로 받아 사용합니다.

res.send()로 웹 브라우저 response에 우리가 입력한 'I am working!!' 이나 'I am robot!!' 을 출력하게 됩니다.

이제 cmd에 __cd 폴더위치__ 를 입력하여 현재 작업중인 폴더로 이동을 시키고 __node index.js__ 입력하여 서버를 실행시켜 봅시다.

server is running on port: 8000 이라고 출력된다면 서버가 실행된겁니다.

Link: [your server][serverlink]

[serverlink]: "http://localhost:8000"

Link: [your server/robot][serverlink]

[serverlink]: "http://localhost:8000/public"

위 링크들을 클릭해서 서버가 실행되었는지 확인해봅시다.

# 4. 정적 파일

이제

```
app.get('/', (req, res) => {
    res.send('I am working!!')
})

app.get('/robot', (req, res) => {
    res.send('I am robot!!')
})
```

부분을 

```
app.use('/public', express.static('./public'))
```

로 바꾸고

* Node 폴더
  * public
    * index.html
  
위와 같은 형식으로 폴더와 그 안에 파일을 만들어줍니다.

index.html 안에는 아무 내용이나 적어도 좋고 눈에 띄일수록 좋습니다.

이제 cmd에서 ctr + c 를 두번 클릭하고 다시 __node index.js__ 를 입력하면 서버가 재시작 되며 변경된 내용이 저장될 겁니다.

Link: [your server/public][serverlink]

[serverlink]: "http://localhost:8000/public"

위 링크를 클릭하면 자신이 작성한 index.html 이 보일 것입니다.

하지만 어째서 index.html 파일을 지정하지도 않고 실행한 것 일까요?

이는 public 폴더의 index.html 파일의 이름과 관련이 있습니다.

웹에서는 __index__ 라는 이름이 굉장히 중요합니다.

다른 프로그래밍 언어의 예약어라고 생각해도 좋습니다.

localhost:8000/public 에 접속하면

```
app.use('/public', express.static('./public'))
```

해당 함수가 실행되는데 첫번째 매개변수는 서버로 통하는 통로(url)를 가르키는 것이고 두번째 매개변수 express.static('./public')) 은 express 오브젝트 즉, 우리가 install 한 express 프레임워크의 static이라는 함수를 실행 시키는 것입니다.

간단하게 이 함수의 내용은 매개변수로 받은 폴더 안의 index 라는 이름의 html 파일을 찾는다고 생각하면 됩니다.

그렇기 때문에 index.html의 파일 위치를 지정하지 않아도 함수로 자동 지정이 된 것입니다.

# 읽을거리
## Node.js에 대하여

Node.js 공식 사이트에선 자신들을

__"비동기 이벤트 주도 javaScript 런타임으로써 Node.js 는 확장성 있는 네트워크 애플리케이션을 만들 수 있도록 설계되었습니다."__ 

라고 소개하고 있습니다.(한글문서 기준)

그렇다면 비동기 이벤트(+1)는 무엇이고 런타임(+2)은 무엇이고 확장성(+3), 네트워크 애플리케이션(+4)은 무엇일까요?

이 모든 걸 설명하기엔 지금 당장 웹 전반과 시스템 동작의 기본까지 내려가야 하는 참사가 벌어질 수도 있기에 요약을 할 필요가 있습니다.

1. 비동기 이벤트
   
   우선 기존의 시스템과 Node.js의 구조 차이를 알아야합니다.

   기존의 서버들은 Blocking I/O 라는 입출력 시스템을 사용하여 멀티 스레드 방식으로 멀티 태스킹을 구현할 수 밖에 없었습니다.

   멀티 스레드 방식에 단점과 함께 장점도 있지만 서버 구동에서 단점이 치명적으로 다가옵니다.

   동시에 여러 요청을 받을 시 멀티 스레드는 요청들을 스케줄링 하여 각 요청이 CPU에서 처리되는 시간을 조정합니다.

   모든 요청이 처리될 때 까지, 혹은 한가지 요청이 처리될 때 까지 애플리케이션은 Blocked 상태. 즉, (I/O, 입출력 혹은 요청을 실행하느라) 멈춰있는 상태라고 생각하면 됩니다.

   이러한 방식이 요청이 많아지는 서버에서 감당하기 힘들고 멀티 태스킹을 위해 CPU를 나눠 쓰기 위해 스케줄링을 하는데도 자원이 소모되니 특정 조건에서 최악의 경우를 보여주게 됩니다.

   Node.js는 이를 해결할 수 있는 구조를 가지고 있습니다.

   Node.js는 싱글 스레드와 이벤트 루프라는 구조를 가지고 있습니다.

   이를 통해 javaScript의 callback 이라는 강점을 살려서 이벤트 루프가 계속 이벤트(I/O, 입출력 또는 요청)를 확인하면서 해당 이벤트가 실행되면 실행이 완료되길 기다리지 않고 워커 스레드라는 장소를 마련하여 별개로 이벤트를 실행시킵니다.

   또한, 이벤트가 끝나는걸 기다리지 않고 이벤트 루프가 다시 해당 이벤트로 돌아가지 않고 다른 요청을 기다립니다.

   바로 callback을 사용하여 미리 정의해둔 함수가 이벤트의 실행 이후에 호출되어 남은 작업을 완료하도록 구현하는 것입니다.

   정리하자면 Node.js로 구현된 애플리케이션은 동기적으로 하나의 요청 혹은 이벤트를 붙잡고 끝날 때 까지 멈춰 있는 것이 아닌 비동기적으로 요청 혹은 이벤트 발생시 단지 실행(워커 스레드)만 시키고 애플리케이션은 동작을 멈추지 않습니다.

   정리하자면 비동기 이벤트는 애플리케이션의 동작을 멈추지 않는 이벤트이고 비동기 이벤트를 주도하는 Node.js가 해당 이벤트를 실행만 시킬 뿐이며 애플리케이션이 해당 이벤트를 끝까지 주관하지 않고 실행 후에 애플리케이션에 callback으로 작업을 되돌려 줄 뿐입니다.

2. 런타임
   
   런타임은 프로그래밍 언어가 구동되는 환경이라고 이해를 하면 됩니다.

3. 확장성
   
   확장성이란 비즈니스 요구 사항에 맞게 확장 하는 시스템의 기능입니다. 기존의 응용 프로그램은 응용 프로그램 대로 확장된 프로그램이 정상적으로 동작하는 기준이기도 합니다.

4. 네트워크 애플리케이션
   
   네트워크 애플리케이션은 두 단어를 나눠서 설명 드리겠습니다.

   네트워크는 컴퓨터들 끼리 통신 기술을 이용하여 그물망처럼 연결된 통신 이용 형태를 의미합니다.

   애플리케이션은 넓은 의미에서는 운영 체제에서 실행되는 모든 소프트웨어를 뜻합니다.

   둘이 합쳐지면 컴퓨터 사이에 통신 기술을 이용하여 상호작용하는 소프트웨어라고 볼 수 있습니다.

그렇다면

__"비동기 이벤트 주도 javaScript 런타임으로써 Node.js 는 확장성 있는 네트워크 애플리케이션을 만들 수 있도록 설계되었습니다"__

의 의미는

__"작업이 끝날 때 까지 기다리지 않는 javaScript 프로그래밍 환경으로써 Node.js 는 비즈니스 요구 사항에 맞게 응용 프로그램 영역을 넓혀가면서 컴퓨터 사이 상호 통신 소프트웨어를 만들 수 있도록 설계되었습니다."__

라고 해석할 수 있습니다.

## javaScript의 접근 제어자에 대하여

javaScript에는 var, const 등 접근 제어자 역할을 하는 예약어가 있습니다.

1. var
   
   var는 쉽게 말해 어디에서나, 계속 이용될 수 있습니다.

   예를 들어,

   ```
   if(조건문) {
     var a = 5;
   }

   console.log(a)
   ```

   위 코드에서 a는 정상적으로 출력됩니다.

   즉, 조건문 내에서 정의된 a의 수명이 조건문 내에서 종료되는게 아니라 계속해서 사용할 수 있게 되는 겁니다.

2. const

   const는 쉽게 말해 한번 값이 정해지면 다시는 값을 새로 저장할 수 없습니다.

   ```
   const a = 5;

   a = 7;
   ```

   위 코드에서 a의 선언 이후 a에 값을 7로 초기화할 때 오류가 납니다.

## 콜백에 대하여

콜백은 어쩌면 javaScript와 .js 파생 시스템들의 가장 핵심이자 중요한 개념이 아닐까 생각합니다.

```
function a (value, callback) {
  console.log('I got ' + value)
  callback()
}

a('root', function() {
  for (i 반복 10번)
    console.log('I am number ' + i)
})
```

위 코드를 차근차근 해석해보면서 콜백의 핵심을 짚어봅시다.

```
function a (value, callback) {
```

함수 a를 선언하였고 두 개의 매개변수를 받을 것입니다.

javaScript에도 명백히 데이터 타입이 존재합니다.

다만, 타입을 명시하지 않기 때문에 달랑 매개변수명만 있는 걸 보고 미리 정의한 변수를 가져다 쓴게 아닌가 하는 착각이 들 수 있습니다.

집중력을 발휘해서 콜백을 공부하는 내내 두 매개변수가 이전에 정의된 변수를 가져다 쓴게 아닌것이란걸 인지해야합니다.

마치 Java의

```
public void a (타입 value, 타입 callback) {

}
```

같다고 생각하시면 됩니다.

```
console.log('I got ' + value)
  callback()
}
```

위 코드를 보면 매개변수로 받은 value 값과 callback이 활용됩니다.

value의 위치와 형태를 보았을 때 어떠한 값이 들어갈 수 있을까요?

정수나, 문자가 들어갈 수 있겠네요.

그렇다면 callback의 위치와 형태를 보았을 때 어떠한 값이 들어갈 수 있을까요?

javaScript의 특징 중 하나는 변수에 함수를 넣을 수 있다는 겁니다.

매개'변수'인 callback의 뒤에 괄호() 가 붙었습니다.

이는 callback이 함수로써 실행되어야 한다는 걸 의미하고, 또 callback 매개변수에는 함수가 들어와야 한다는 걸 증명하는 것이나 마찬가지입니다.

그럼 a를 호출하는 부분을 봅시다.

```
a('root', function() {
  for (i 반복 10번)
    console.log('I am number ' + i)
})
```

위 코드를 보았을 때 매개변수 value에는 root라는 문자를 값으로 주었습니다.

매개변수 callback에는 I am number '0~9' 라고 출력하는 함수를 값으로 주었습니다.

다시 구현부를 봅시다.

```
console.log('I got ' + value)
callback()
```

우선 매개변수 value 값을 사용하여 console.log를 실행하겠네요.

'I got root' 가 출력됩니다.

이후엔 매개변수 callback 이라는 함수를 실행해야합니다.

'I am number 0'

'I am number 1'

'I am number 2'

. . .

'I am number 9'

위와 같이 출력될 것입니다.

그럼 만약 callback 값에 숫자나 문자 값을 주면 어떻게 될까요?

함수 a에서 매개변수 callback을 함수로써 실행했기에 함수로써 실행될 수 없는 숫자나 문자가 들어오면 오류를 일으킵니다.

정말 간단하게 콜백을 살펴보자면 이런 용도가 있고 이정도 방법이 있다고 설명할 수 있습니다.

하지만, 실제로 콜백의 용도와 구현 방법은 무궁무진하고 javaScript나 js 파생 시스템 계열에서 너무도 흔한 프로그래밍 기법입니다.

만약, 콜백의 용도를 Node.js 에 대한 내용과 함께 알고 싶다면 위에 있는 'Node.js에 대하여'를 읽어주세요.

# 10월 15일자 수업

# 1. 비동기 처리(Promise, async, await)에 대하여

비동기 처리는 쉽게 말해 특정 코드의 연산(실행)이 끝날 때까지 전체 코드의 흐름을 멈추지 않고 다음 코드를 먼저 실행하는 방식을 의미합니다.

우선 Web Api의 한 종류인 setTimeout() 을 예시로 설명하겠습니다.

```
console.log('Hello')

setTiemeout(function() {
  console.log('Work')
}, 5000)

console.log('Bye')
```

결과는

```
// #1

Hello 출력
Bye 출력
(5초 후에)
Work 출력
```

setTimeout() 의 두번째 인자로 전달된 5000(ms단위)이라는 값으로 인하여 JavaScript 런타임이 setTimeout() 을 조우한 시점에서 첫번째 인자로 전달된 함수를 실행시키기 까지 5초가 걸립니다.

그렇다면 상식적으로

```
// #2

Hello 출력
(5초 후에)
Work
Bye
```

와 같은 결과가 나와야 하는데 #1과 같은 결과가 나온 이유는 setTimeout() 이 자체적으로 비동기 처리가 되어있어 특정 코드의 연산(실행)이 끝날 때까지 멈춰있지 않고 다음 코드를 먼저 실행하기 때문입니다.

(* 참고: Web Api는 웹 환경에서 사용할 수 있는 API(Application Programing Interpace)로 개발자가 시스템의 일부를 구현하는 수고를 덜어주고 플랫폼 환경이나 클라이언트 환경에 제한되지 않고 웹 환경에서 동작합니다.)

비동기 처리와 연관 깊은 개념으로는 callback 패턴이 있습니다.

개발자의 입장에서나 사용자의 입장에서나 특정 행동이 완료된 후에 다음 행동으로 넘어가길 원할 때가 있습니다.

그럴 때 callback 패턴으로 원하는 동작을 구현할 수 있습니다.

```
# 3

function setting() {
    let data = 'no data'
    setTimeout(function() {
        data = 'data'
    }, 3000)
    return data
}

console.log(setting())

결과: no data 출력
```

우리가 원하는 결과는 data에 'data'라는 값이 들어간 후에 그 값이 출력되는 것입니다.

하지만 setTimeout() 은 비동기 처리된 함수이기 때문에 data에 새로운 값을 할당하기 전에 return되어 console.log() 로 출력됩니다.

그리고 JavaScript 런타임이 setTimeout() 을 조우한 시점에서 3초가 지난 후에야 data의 값을 새로이 할당합니다.

```
# 4

function setting(callbackFunc) {
  // 1. 인자로 받은 callbackFunc가 어떤 타입인지 어떤 용도인지 '인자를 받겠다' 라고 선언한 시점에선 모릅니다.
    let data = 'no data'
    setTimeout(callbackFunc(data), 3000)
    // 2. callbackFunc의 뒤에 () 괄호가 붙으면서 함수라는 것이 정의됩니다.
}

setting(function(data) {
    // 3. setting의 인수로 넘겨줄 callbackFunc가 함수의 형태라는 것을 알았으니 함수를 만들어 인수로 넘겨줍니다.
    data = 'data'
    console.log(data)
})

결과: data 출력
```

이를 위의 코드와 같이 callback 패턴을 사용하여 선처리가 필요한 작업을 한 후에 다음 행동을 콜백 함수로 실행하여 문제 없이 원하는 동작을 실행시킬 수 있습니다.

(* 참고: 인자의 이름이나 변수의 이름과는 관계 없이 #4와 같은 함수 사용법을 callback 패턴이라고 부릅니다.)

이런 비동기 처리 로직을 위해 콜백 함수를 연속해서 사용할 때 발생하는 문제들이 있습니다.

```
$.get('url', function(response) {
	parseValue(response, function(id) {
		auth(id, function(result) {
			display(result, function(text) {
				console.log(text);
			});
		});
	});
});
```

서비스를 개발하다 보면 서버에서 데이터를 받아와 화면에 표시하기까지 여러 과정을 거칩니다. 이 모든 과정이 비동기로 처리되야 한다면 위와 같이 콜백 안에 콜백이 물고 늘어지는 식의 코드가 짜여지게 됩니다.

이러한 구조는 가독성도 떨어지고 로직 변경도 어렵습니다. 위와 같은 코드 구조를 흔히 콜백 지옥이라고 합니다.

Promise와 async, await의 개념을 알면 콜백 지옥을 해결할 수 있습니다.

## Promise

Promise는 JavaScript 비동기 처리에 사용되는 객체입니다.

Promise는 주로 서버에서 받아온 데이터를 화면에 표시할 때 사용합니다. 만약 비동기 처리 된 함수나 API를 실행하여 데이터를 받아오기도 전에 화면에 데이터를 표시하려 한다면 오류가 발생하거나 개발자 혹은 사용자가 원치 않았던 상황이 벌어질 것입니다. Promise를 사용하여 이러한 문제를 해결할 수 있습니다.

```
function setting(callbackFunc) {
    let data = 'no data'
    setTimeout(callbackFunc(data), 3000)
}

setting(function(data) {
    data = 'data'
    console.log(data)
})
```

위 코드는 data의 값을 'data'로 재할당하고 출력해주는 코드에 callback 패턴을 적용한 모습입니다.

```
function setting() {
    let data = 'no data'
    return new Promise([1]function(resolve, reject) {
      data = 'data'
      setTimeout(function() {
        resolve(data)
      }, 3000)
    })
}

setting().then([2]function(data) {
  console.log(data)
})
```

위 코드는 Promise 객체를 이용하여 코드를 작성했습니다. Promise 생성자에 [1]함수를 인자로 전달합니다. 또 인자로 받은 [1]함수에는 두개의 인자를 받는데 각각 resolve와 reject입니다. data의 값을 'data'로 재할당하고 setTimeout으로 3초 뒤에 resolve 함수 즉 then의 인자로 받은 [2]함수를 실행시켰고 resolve에 전달한 인자가 그대로 then의 인자로 받은 [2]함수의 인자로 전달된 모습을 볼 수 있습니다.

(* 참고: 실제 코드를 구동할 때는 [] 부분은 삭제해야합니다.)

Promise 객체를 사용할 때 알아야 하는 가장 기본적인 개념이 바로 Promise의 상태(states)입니다. 여기서 말하는 상태란 Promise의 처리 과정을 의미합니다. new Promise() 생성자로 Promise 객체를 생성하고 종료될 때까지 3가지 상태를 갖습니다.

* Pending(대기): 비동기 처리 로직이 아직 완료되지 않은 상태

* Fulfilled(이행): 비동기 처리가 완료되어 Promise가 결과 값을 반환해준 상태

* Rejected(실패): 비동기 처리가 실패하거나 오류가 발생한 상태

## 1. Pending(대기)

```
new Promise();
```

위와 같이 Promise 객체의 생성자를 호출하면 Pending(대가) 상태가 됩니다.

```
new Promise(function(resolve, reject) {
  . . .
})
```

생성자를 호출할 때 콜백 함수를 선언할 수 있고, 콜백 함수의 인자로 resolve, reject를 받습니다.

## 2. Fulfilled(이행)

여기서 콜백 함수의 인자 resolve 함수를 아래와 같이 실행하면 Fulfilled(이행) 상태가 됩니다.

```
new Promise(function(resolve, reject) {
  resolve()
})
```

이행 상태가 되면 아래와 같이 then() 을 이용하여 처리 결과 값을 받을 수 있습니다.

```
function gettingData() {
  return new Promise(function(resolve, reject) {
    let data = 50
    resolve(data)
  })
}

gettingData().then(function(resolveData) {
  console.log(resolveData)
})

결과: 50
```

resolve 함수를 실행하면 then에 있는 콜백 함수가 실행되는 걸 보실 수 있습니다.

## 3. Rejected(실패)

new Promise() 생성자로 Promise 객체를 생성하면 콜백 함수 인자로 resolve와 reject를 전달 받습니다. reject를 호출하면 Rejected(실패) 상태가 됩니다.

```
new Promise(function(resolve, reject) {
  reject()
})
```

위와 같이 reject 함수가 실행할 수 있습니다.

```
function gettingData() {
  return new Promise(function(resolve, reject) {
    reject(new Error("OMG SUPER ERROR HAS BEGAN"))
  })
}

gettingData().then().catch(function(err) {
  console.error(err)
})

결과: Error : OMG SUPER ERROR HAS BEGAN
```

resolve가 then으로 연결되듯이 reject가 생성한 Error 객체는 catch로 연결되어 콜백 함수를 실행시킵니다.

배운 내용을 바탕으로 몇가지 예제를 봅시다.

```
function gettingData() {
  let data
  return new Promise(function(resolve, reject) {
    data = 'data'
    setTimeout(function() {
      if (data != null) {
        resolve(data)
      }
      reject(new Error("OMG SUPER ERROR HAS BEGAN))
    }, 3000)
  })
}

gettingData().then(function(data) {
  console.log(data)
}).catch(function(err) {
  console.error(err)
})
```

위 코드는 data의 값이 null이 아니면 then의 콜백 함수를 실행시켜 data를 출력하고 null이라면 catch의 콜백 함수를 실행시켜 인자로 전달받은 Error 객체를 출력합니다.

```
function gettingData() {
  return new Promise({
    . . .
  })
}

gettingData()
  .then(function(data) {
    . . .
  })
  .then(function(data) {
    . . .
  })
  .then(function(data) {
    . . .
  })
```

위의 코드와 같은 구조로 then을 여러개 연결하여 코드를 구성할 수도 있습니다.

실제로는 아래와 같이 작성합니다.

```
function gettingData() {
  return new Promise(function(resolve, reject) {
    setTimeout(function() {
      resolve(1)
    }, 2000)
  })
}

gettingData()
  .then(function(data) {
    console.log(data) // 1
    return data + 10
  })
  .then(function(data) {
    console.log(data) // 11
    return data + 20
  })
  .then(function(data) {
    console.log(data) // 31
  })

결과:
1 출력
11 출력
31 출력
```

위 코드의 then은 계속 이어지면서 return 받은 값을 받거나 혹은 받지 않고 실행된다.

```
let userData = {
  id: 'testID',
  pw: 'testPW'
}

function parseVal() {
  return new Promise({
    // 데이터를 파싱하는 내용
  })
}

function auth() {
  return new Promise({
    // 인증하는 내용
  })
}

function screen() {
  return new Promise({
    // 화면을 나타내는 내용
  })
}

testMethod(userData)
  .then(parseVal)
  .then(auth)
  .then(screen)
```

위와 같이 유저의 정보를 이용하여 필요한 동작을 then을 통해 연속적으로 거쳐서 수행할 수 있습니다.

## async & await

async와 await은 기존의 비동기 처리 방식인 callback 패턴과 Promise의 단점을 보완하고 개발자가 읽기 좋은 코드를 작성할 수 있게 도와줍니다.(확장성 증가)

```
function logName() {
  let user = fetchUser('domain.com/users/1')
  if (user.id === 1) {
    console.log(user.name)
  }
}
```

위 코드의 fetchUser() 함수는 서버에서 데이터를 받아오는 HTTP 통신 코드라고 가정합니다. 

일반적으로 JavaScript의 비동기 처리 코드는 아래와 같이 콜백을 사용해야 코드의 실행 순서를 보장 받을 수 있습니다.

```
function logName() {
  let user = fetchUser('domain.com/users/1', function(user) {
    if (user.id === 1) {
      console.log(user.name)
    }
  })
}
```

callback 패턴에 익숙해진 사람이라면 위와 같은 방식을 어려워하지 않겠지만, 익숙하지 않은 사람 혹은 더욱 직관적인 구조를 원하는 사람들에겐 불편할 수도 있고 고려해야할 상황이 많아져 코드를 해석하는것이 어려울 수도 있습니다.

```
async function logName() {
  let user = await fetchUser('domain.com/users/1')
  if (user.id === 1) {
    console.log(user.name)
  }
}
```

위 코드는 원래 코드에 async와 await의 개념을 적용하여 우리가 바라는 동작을 callback 패턴을 사용하지 않고 자연스래 동작해줍니다.

async와 await를 더 자세하게 알아봅시다.

```
async function 함수() {
  await 비동기 처리 함수()
}
```

전체 동작을 통솔하는 함수의 앞에 async 예약어를 달아줍니다. 그 후에 비동기 처리가 필요한 함수 앞에 await 예약어를 달아줍니다. 주의해야할 점은 비동기 처리 함수가 반드시 Promise 객체를 반환해야 await의 동작이 의도한 대로 흘러갑니다.

몇가지 예제 코드를 더 살펴보겠습니다.

```
function fetchItems() {
  return new Promise(function(resolve, reject) {
    let items = [1,2,3]
    resolve(items)
  })
}

async function logItems() {
  let resultItems = await fetchItems()
  console.log(resultItems)
}
```

fetchItems() 함수는 Promise 객체를 반환하는 함수입니다. Promise 객체는 JavaScript 비동기 처리를 위해 존재합니다. fetchItems() 함수를 실행하면 Promise 객체가 Resolved(이행) 상태가 되며 return 값은 items 변수의 배열이 됩니다.

logItems() 함수는 fetchItems() 함수의 return 값인 items 배열이 resultItems 변수에 담깁니다.

따라서 [1,2,3] 이 출력됩니다.

await을 사용하지 않았다면 데이터를 받아온 시점에 console을 출력할 수 있도록 callback 패턴이나 .then() 등의 방식을 사용해야 했을 겁니다. 하지만 async, await 문법 덕에 비동기 처리에 대한 사고를 온종일 하고 있지 않아도 되게 된것입니다.

이 실용적인 문법이 가장 효율적으로 이용되는 순간은 여러 개의 비동기 처리 코드를 다룰 때입니다.

```
function fetchUser() {
  let url = 'https://domain.type.com/user/1'
  return fetch(url).then(function(response) {
    return response.json()
  })
}

function fetchTodo() {
  let url = 'https://domain.type.com/user/1'
  return fetch(url).then(function(response) {
    return response.json()
  })
}
```

위 함수들은 각각 사용자의 정보와 할 일에 대한 정보가 담긴 Promise 객체를 반환한다고 가정해봅니다.

이 두 함수를 이용하여 할 일의 제목을 출력한다고 하면 아래와 같은 로직이 필요합니다.

1. fetchUser() 를 이용하여 사용자 정보 호출

2. 받아온 사용자 아이디가 1이면 할 일 정보 호출

3. 받아온 할 일 정보의 제목을 console에 출력

```
async function logTodoTitle() {
  let user = await fetchUser() // 1
  if (user.id === 1) { // 2
    let todo = await fetchTodo()
    console.log(todo.title) // 3
  }
}
```

logTodoTitle() 을 실행하면 console에 할 일의 제목이 출력될 것입니다. 위 비동기 처리 코드를 callback 패턴이나 Promise 객체만으로 처리 했다면 훨씬 코드가 길어졌을 것이고 불필요하게 반복되는 코드의 출현이나 가독성 하락 등 좋지 않은 상황이 연출되었을 겁니다. 이처럼 async, await 문법을 이용하여 코드의 가독성도 높이고 직관적인 구조를 형성할 수 있는 장점이 생깁니다.

async & await의 예외처리는 try catch 방식으로 처리합니다.

```
async function logTodoTitle() {
  try {
    let user = await fetchUser()
    if (user.id === 1) {
      let todo = await fetchTodo()
      console.log(todo.title)
    }
  } catch (error) {
    console.log(error)
  }
}
```

위의 코드를 실행하면 동작 중 발생한 네트워크 오류뿐만 아니라 간단한 타입 오류 등의 일반적인 오류까지도 catch로 잡아냅니다. 발견된 에러는 error 객체에 담기기 때문에 에러 유형에 맞는 에러 코드를 처리해주면 됩니다.

# 2. GET, POST 방식에 대하여

HTML의 form 태그를 보면 method라는 요소가 있고 GET값과 POST값을 줄 수 있습니다.

대부분의 애플리케이션의 기본이 되는 CRUD(Create Read Update Delete) 중에 각각 C(POST)와 R(GET)의 역할을 합니다.

역할이 다르기 때문에 form 태그의 method 요소에 어떤 값이 들어가냐에 따라 form 태그에서 데이터를 전송하는 방식도 달라집니다.

흔히 GET 방식은 'url?id=myId&pw=myPw' 이러한 형식을 취합니다.

사용자에게 사용자가 어떤 값을 전송했는지 훤히 보여주는 셈입니다. 또한 전송 받은 데이터로 어떤 작업을 할지도 예측할 수 있습니다.

평소엔 별 문제가 없겠지만 만약 우리가 url을 누군가에게 전송해야 합니다. 혹은 공유해야 할 상황입니다. 자신의 아이디와 비밀번호 혹은 노출되어선 안되는 정보가 타인에게 노출될 수 있습니다.

이러한 GET 방식은 자신이 어떤 데이터를 읽어들였고 타인에게 자신이 어떤 데이터를 읽어들였는지 공유할 때는 유용하겠지만 개인적인 정보, 공유되어선 안되는 정보가 포함될 때는 적합하지 않습니다.

때문에 개인정보나 그 외 여러 중요한 정보들은 POST 방식으로 데이터가 전송됩니다.

GET 방식으로 전송하던 데이터를 POST 방식으로 전송한다고 해서 특별히 눈에 뛰는건 url 라인에 사용자가 전송한 데이터가 보이지 않는다는 것 뿐이고 이는 개발자 혹은 사용자가 의도한 행동입니다.

하지만 여기서 기존 코드에 문제가 발생합니다.

데이터를 받는 쪽에서도 받는 방식이 달라집니다.

즉 데이터를 받아서 표현 혹은 사용하는 방법에 변화를 주어야 합니다.

Node.js의 express 프레임워크를 예시로 들자면

```
// 기존
const express = require('express')
const app = express()

// 추가
app.use(express.json())
app.use(express.urlencoded())
```

위 코드를 추가하여 express 객체를 담은 app의 기능을 업데이트 해야만 새로운 방식으로 데이터를 받을 수 있습니다.

```
app.post('/robot', function (req, res) {
  const { body: { id, pw} } = req
  res.send(`title is ${id} name is ${pw}`)
})
```

app의 함수를 사용할 때도 app.get이 아닌 app.post로 데이터를 받아야하고 데이터를 사용할 때도 'const { body: { id, pw} } = req' 와 같이 한층 복잡한 과정을 거칩니다.

위 코드를 해석하자면 form 태그의 action으로 혹은 사용자의 요청으로 'domain/robot'으로 이동했을 때 POST 방식으로 데이터(req/requst 즉 요청)를 받을 것이고 전달 받은 데이터(req) 속 form 에 입력 받은 'name=id' 와 'name=pw'의 데이터를 변수로 저장하겠다는 의미입니다.

반환(res/response)할 때 'title is ${id} name is ${pw}' 즉, 문장에 사용자가 입력한 데이터를 반영하여 출력합니다.

# 읽을거리

## nodemon을 활용한 변경 내용 실시간 반영

npm의 서비스 중 nodemon을 활용하여 서버를 자동으로 저장하고 실시간 변경사항을 반영할 수 있습니다.

우선 작업하는 폴더로 이동하여 터미널에

```
npm init
```

입력하여 package.json 파일의 생성을 돕습니다.

(* 참고: 작업중인 폴더명에 한글이 섞이면 오류가 발생할수도 있습니다.)

```
npm install nodemon
```

을 입력하여 추가적으로 nodemon에 대한 정보를 npm package에 담습니다.

```
npm install --save-dev nodemon
```

을 입력하면 설치된 nodemon이 package.json 파일에서 "devDependencies" 의 아래로 이동한걸 볼 수 있습니다.

package.json 파일에서 "scripts" 부분에 "dev"를 추가하고 아래와 같이 설정합니다.

```
"scripts": {
    . . .
    "dev": "nodemon 현재 폴더를 기준으로 실행할 js파일의 위치",
    . . .
  }
```

이렇게 설정하고 현재 작업중인 폴더의 터미널에 npm run dev를 입력하면 "scripts" 에 설정한 "dev" 명령어가 발동하며 서버를 재시작하지 않아도 코드의 변경내용이 실시간으로 적용됩니다.

## 화살표 함수

화살표 함수로 함수를 더욱 간단하게 만들 수 있습니다.

평소에 JavaScript에서 함수를 만들 때는

```
let func = function(par1, par2, par3, . . .) {
  return anyData
}
```

위와 같은 방식을 사용합니다.

화살표 함수를 사용하면

```
let sumInt = function(a, b) {
  return a + b
}

console.log(sumInt(1, 2))

결과: 3
```

이러한 함수를

```
let sumInt = (a, b) => a + b

console.log(sumInt(1, 2))

결과: 3
```

이렇게 변형하여 더 간결하게 코드를 작성할 수 있습니다.

명시적으로 return을 하지 않았음에도 화살표로 가르킨 계산의 결과를 반환합니다.

* 인수가 하나뿐이라면 인수를 감싸는 괄호를 생략할 수 있습니다.

```
let sum = n => n + 1

console.log(sum(3))

결과: 4
```

* 인수가 하나도 없다면 괄호를 비워둘 수 있습니다. 하지만 괄호를 생략할 순 없습니다.

```
let sum = () => 1 + 2

console.log(sum())

결과: 3
```

이러한 방식을 활용하여 더욱 동적이지만 간결한 함수를 만들 수 있습니다.

```
let age = 18

let welcome = age => {
  (age < 18) ? console.log(`${age}살이구나 안녕!`) : console.log(`${age}살이시군요 안녕하세요!`)
}

welcome(age)

결과: 18살이시군요 안녕하세요!
```

또한 여러 줄의 화살표 함수를 쓸 때는 중괄호로 감싸야 하며 명시적으로 return을 반환해주어야 합니다.

```
let sum = (a, b) => {
  let result = a + b
  return result
}

console.log(sum(1, 2))

결과: 3
```

이처럼 다양한 방식으로 화살표 함수를 활용할 수 있고 익숙해지면 다양한 동작을 간결하게 구현할 수 있습니다.

## 종하야  
