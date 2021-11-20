---
title: "[Jetpack Compose] 2021.11.20 State"
date: 2021-11-20T15:34:30-04:00
classes: wide
categories:
  - Android
tags:
  - Android
  - Jetpack Compose
---

**Warning Notice:** 이 글은 개인적인 학습을 위해서 정리한 내용입니다. 틀린 내용이 있을 수 있습니다.
{: .notice--warning}

## State 란?

시간에 따라서 변할 수 있는 모든 값. ex) 변수, 애니메이션 상태, DB

## Unidirectional Data Flow

data 를 한 방향으로만 흐르게 하는 구조. 

기존 안드로이드 View System 에서는 View 객체 내부에서도 State 값을 가진다. 이 State Data 는 이벤트 핸들러에 의해서 상위로 전달되어 다른 구조(예를 들어 ViewModel)에 저장되어 있는 State 값을 갱신한다. 또는 다른 구조에서 데이터를 View 에 전달하여 화면을 갱신하기도 한다. 이렇듯 Android View System 에서는 Data 가 양방향으로 흐를 수 있다.

이런 구조의 문제점은 서로 다른 지점에서 관리 되고 있는 2개 이상의 State 들에 대한 Sync 를 맞춰줘야 한다는 점이다. 이런 sync 작업은 개발자에게 달려 있으며, 화면 UI 가 복잡해질 수록 어느 한 부분에서 Sync 작업을 놓치게 될 수도 있다.

Unidirectional Data Flow 를 추구하는 Jetpack Compose 에서는 Composable 함수 내부에서 State Data 를 가지지 않는다. 대신 매개변수를 통해서 전달 받는다. 또한 이 데이터를 갱신하는 이벤트 또한 이를 위쪽으로 전달할 수 있는 람다 함수 형태의 매개변수를 받아서 전달하게 된다. 데이터는 Composable 안으로, 데이터를 갱신하는 이벤트는 Composable 밖으로 보내는 구조를 통해 Unidirectional Data Flow 구조를 가지게 된다.

## Memory In Composable

근본적으로 Composable 함수 내부에서는 어떤 데이터를 저장할 수 없다. 왜나하면 함수이기 때문에 함수 호출이 종료되고 나면 함수 내부의 로컬 변수들은 모두 메모리 Stack 에서 Pop 되기 때문이다. 그러나 Jetpack Compose 라이브러리를 통해 마치 객체 내부의 멤버 변수를 두는 듯이 Composble 함수 내부에 메모리를 두어 데이터를 저장할 수 있다.

```kotlin
fun FooComposable(someData: Data) {
    val barInt: Int = remember(someData.id) { someComputation(someData.value) }
}
```

- remember 키워드는 인자로 전달 받은 키 값을 바탕으로 데이터를 저장할 수 있게 해준다. 마지막 매개변수는 computation 으로 저장할 데이터값을 계산하는 람다를 말한다.
- 이 Composable이 Recomposition 될 때마다 barInt 값이 새로 초기화 되는 것이 아니라 key 값으로 전달한 데이터가 바뀌지 않는한 최초에 초기화 되었던 값을 유지하게 된다.

이같은 데이터는 Composable이 Composable Tree 상에 유지될때만 남아있게 된다. Lazy Column 과 같은 Composable 내부에서는 화면에 보이는 Composable 만 유지하기 때문에 화면 밖으로 나가는 Composable 들은 Tree 상에서 제거된다. 따라서 이같은 Composable 내부에서 remember를 사용하더라도 데이터를 유지할 수 없기 때문에 remember를 통한 데이터 유지는 중요하지 않는 데이터에 대해서만 수행하는 것이 좋다.

## Stateful Composable

근본적으로 built-in Composable 들은 내부에 상태를 저장하지 않는다(Stateless). 특정한 목적을 위해 내부에 상태를 저장하는 Composable 을 생성할 수 있는데 이를 Stateful Composable 이라고 한다. remember 키워드와 함께 만들 수 있다.

```kotlin
fun SomeStatfulComposable() {
    val state = remember { mutableStateOf("") }
    val state: String by remember { mutableStateOf("") }
    val (state, setState) = remember { mutableStateOf("") }
}
```

## State Hoisting

Composable 내부의 State를 Caller 쪽으로 이동 시키는 것을 의미한다. 보통 해당 State 의 Data 를 전달받기 위한 매개변수와 해당 State를 변경 시킬 수 있는 이벤트를 전달하기 위한 람다 함수 매개변수를 정의하는 것으로 State Hoisting 이 달성된다. 이를 통해 Stateless Composable 을 만들 수 있으며 재사용성, 테스트 가능성 향상과 같은 장점이 있다.

State Hoisting 은 다음과 같은 장점이 있다.

- Composable Tree 상에서 자식들이 부모로 Hoisting 된 State 를 공유하여 사용할 수 있다.
- State Encapsulation 효과가 있다. State 를 갱신하려는 이벤트를 중간에 Intercept 하여 이를 무시하거나, 적절한 validation을 수행하거나 하는 등의 처리가 가능하다.