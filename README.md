#gava Objective-C Coding Style Guide

 이 스타일 가이드는 개인적으로 iOS 플랫폼의 프로젝트를 진행할 때 길라잡이로 쓰기 위해 작성 중인 가이드입니다. 이 가이드는 [애플의 코코아 코딩 가이드라인](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/CodingGuidelines/CodingGuidelines.html)에 의거하여 작성되었으며, [NYTimes Objective-C Style Guide](https://github.com/NYTimes/objective-c-style-guide) 등 다른 가이드라인들을 참고하였습니다.

## 목차
* [기본 원칙](#기본-원칙)
	* [가독성을 최우선으로](#가독성을-최우선으로)
	* [최대한 자연어에 가깝게](#최대한-자연어에-가깝게)
	* [축약어를 최대한 배제](#축약어를-최대한-배제)
* [띄어쓰기](#띄어쓰기)
    * [Tab 대신 4칸의 Spaces로](#Tab-대신-4칸의-Spaces로)
    * [메소드 공백](#메소드-공백)
* [같이 보기](#같이-보기)


## 기본 원칙
### 가독성을 최우선으로
* #####최대한 자연어에 가깝게

 ```objc
 [nameTextField becomeFirstResponder]
 ```
 위 코드를 보면, 문법에 따라 ```"이름 텍스트필드가 첫번째 Responder가 되어라"```라고 자연스럽게 읽히게 됩니다.

 Objective-C 언어는 되도록이면 자연어처럼 읽히게 하고자 하는 철학을 지향하는 언어입니다.이는 코더의 가독성을 제고하는 효과가 있고, 가독성의 개선은 유지보수의 효율성을 높이는 데 도움이 됩니다.

* #####축약어를 최대한 배제

 **Good**
 ```objc
 UITextField *nameTextField;
 WriteViewController *writeViewController;
 - (void)invokeMethod:(selector)aMethod;
 ```
 **Bad**
 ```objc
 UITextField *nameTF;  // Textfield? TaskForce?
 WriteViewController *writeVC; // writeVirtualController?
 - (void)IM:(selector)aMethod; // IM is a LOL TEAM. lol
 ```
 
 클래스 이름이나 변수, 메소드 이름을 만들 때, 축약어를 쓰지 않도록 합니다. 이는 위에 적은 "최대한 자연어에 가깝게"라는 원칙과 맞닿아있고, 또한 축약을 통해 생길 수 있는 모호한 해석을 방지하는 데도 도움이 됩니다. 
  
 다만 몇 가지 예외를 둘 수 있는데,
 
 - 아주 잘 알려진 용어들(```app```, ```alloc```, ```init```, ```rect```, ```temp``` 등)
 - 메소드의 인자 이름
 - 클래스 앞의 Prefix(**``NS``**Object, **``CG``**Float 등)

 등은 축약어를 써도 가독성에 무리가 적거나, 축약어가 필요한 경우입니다.

 **SEE ALSO**:
 * [Coding Guidelines for Cocoa - Code Naming Basics](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/CodingGuidelines/Articles/NamingBasics.html)
 * 예외의 예시는 [Coding Guidelines for Cocoa - Acceptable Abbreviations and Acronyms](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/CodingGuidelines/Articles/APIAbbreviations.html)를 참고 바랍니다.


## 띄어쓰기

* #####Tab 대신 4칸의 Spaces로

 Xcode의 `Preferences` 메뉴에서 `Text Editing` -> `Indentation` 탭을 선택하면 Tab 키를 누를 때의 동작을 선택할 수 있습니다. *Indent in leading whitespace*가 기본값이므로, 기본값 상태에서 Tab 키를 누르면 자동으로 탭 문자 대신 스페이스 4칸이 들어갑니다.

* #####메소드 공백
 - **클래스 지정자(`-`/`+`) 뒤에는 Space 한 칸이 붙습니다.**

    **Good**

	```objc
	- (void)methodName:(NSString *)nameString
	```

    **Not Good**

	```objc
	-(void)methodName:(NSString *)nameString
	```

 - **반환 타입(```BOOL```, ```NSObject``` 등) 뒤에는 Space가 붙지 않습니다.**

    **Good**

	```objc
	- (void)methodName:(NSString *)nameString
	```

    **Not Good**

	```objc
	-(void)methodName:(NSString *)nameString
	```

 - **`메소드 이름`과 `첫 파라미터의 타입`, 그리고 `파라미터 이름` 앞에는 Space가 붙지 않습니다. **

    **Good**

	```objc
	- (void)methodName:(NSString *)nameString
	```

	**Not Good**

	```objc
	- (void)methodName: (NSString *)nameString
	```			
	
	**Not Good**

	```objc
	- (void)methodName:(NSString *) nameString
	```

 - **메소드 파라미터들 사이에는 Space 한 칸을 띄워줍니다.** 

    **Recommended**

	```objc
	- (void)methodName:(NSString *)nameString infoArray:(NSArray *)infoArray
	```

   파라미터 이름이 너무 길거나 파라미터 개수가 3개 이상이라 가독성에 지장을 줄 가능성이 높은 경우에는 파라미터들을 개행으로 구분하는 것을 권장합니다.

	**Recommended**

	```objc
	- (void)methodWithString:(NSString *)aNameString
				informations:(NSDictionary *)informations
				        flag:(bool)flag
	{
		return;
	}
	```	
	
	이 점은 메세지를 보낼 때(메소드를 사용할 때)에도 마찬가지입니다.
		
	**Recommended**

	```objc
	[object methodWithString:myName
				informations:informations
				        flag:YES];
	```




## 같이 보기