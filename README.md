# Menu Class
메뉴를 미리 정의된 객체로 생성합니다.

## Installation
아래 두가지 방법중 하나를 선택하여 설치하세요. 먼저 [git](https://git-scm.com/download/win)이 설치되어 있어야 합니다.

오토핫키 스크립트로 설치하는 방법:
```ahk
; 표준 라이브러리에 설치
RunWait git clone https://github.com/neovis22/menu.git, % a_ahkPath "\..\Lib"

; 로컬 라이브러리에 설치
RunWait git clone https://github.com/neovis22/menu.git Lib/menu
```

사용할 스크립트에 아래 코드를 추가하세요.
```ahk
#Include <menu\menu>
```

## Usage

#### 기본 사용법
```ahk
myMenu := menu([
(join ltrim
    {name:"First"},
    {name:"Second", menu:[
        {name:"Submenu item 1"},
        {name:"Submenu item 2"}
    ]},
    {name:"Third"}
)])

if (item := myMenu.show())
    MsgBox % item.name
```
첫번째 매개변수로 메뉴 아이템으로 이루어진 배열을 전달합니다.

콜백 함수를 지정해서 이벤트를 처리하거나 `show()`메서드에서 선택된 아이템을 리턴받아 곧바로 이벤트를 처리할 수 있습니다.
콜백함수는 `menu`함수의 두번째 매개변수로 전달하여 모든 이벤트를 받거나 메뉴아이템의 `callback`속성으로 메뉴 아이템마다 이벤트를 처리할 수 있습니다.

#### Gui
```ahk
menuBar := menu([
(join ltrim
    {name:"&File", menu:[
        {name:"Open File`tCtrl+O"},
        {name:"Save`tCtrl+S"},
        {name:"Save As`tCtrl+Shift+S"},
        {},
        {name:"Close File`tCtrl+W"},
        {},
        {name:"Exit"}
    ]},
    {name:"&Edit", menu:[
        {name:"Copy`tCtrl+C"},
        {name:"Cut`tCtrl+X"},
        {name:"Paste`tCtrl+V"}
    ]},
    {name:"&View", menu:[
        {name:"Tabs", checked:true},
        {name:"Menu Bar", checked:true},
        {name:"Status Bar", checked:true}
    ]},
    {name:"&Help", menu:[
        {name:"Document`tF1"},
        {},
        {name:"About"}
    ]}
)], "menuBarEvent")

menuBarEvent(item, index, menu) {
    MsgBox % Format("Name: '{}'`nIndex: {}", item.name, index)
}

Gui New
Gui Menu, % menuBar.name
Gui Show, w600 h400
```
메뉴를 생성한 객체가 소멸되면 메뉴가 자동으로 제거되므로 객체를 유지시켜야합니다.

메뉴아이템의 `name`속성이 비어있을 경우 구분줄로 추가됩니다.

## Constructor
- `menu(menuItems, callback="")`
    - `menuItems`
    - `callback(item, index, menu)`
        - `item` 선택된 메뉴 아이템 객체
        - `index` 메뉴 아이템의 순서
        - `menu` 메뉴 객체

## Methods
- `delete(itemName)`
- `rename(itemName, newName="")`
- `check(itemName)`
- `uncheck(itemName)`
- `toggleCheck(itemName)`
- `enable(itemName)`
- `disable(itemName)`
- `toggleEnable(itemName)`
- `setColor(itemName, color="", applyToSubmenus="")`
- `setIcon(itemName, fileName, iconNumber="", iconWidth="")`
- `noIcon(itemName)`
- `show(x="", y="")`

## Properties
- `default`
- `handle`

## Objects

#### Menu
- `MenuItem`으로 이루어진 배열

#### MenuItem
- `name` 메뉴 아이템으로 표시할 문자열
- `checked`
- `disabled`
- `color`
- `icon` `{file, [number], [width]}`
- `default`
- `options` `Menu Add`에서 마지막 매개변수로 입력하는 옵션
- `callback`
    - `callback(item, index, menu)`
        - `item` 선택된 메뉴 아이템 객체
        - `index` 메뉴 아이템의 순서
        - `menu` 메뉴 객체
- `menu` 하위메뉴 아이템의 배열

## Features
- 메뉴 아이템에 `checked`속성이 존재할 경우 자동으로 상태를 토클하고 아이템 객체를 업데이트

## Contact
[카카오톡 오픈 프로필](https://open.kakao.com/me/neovis)
