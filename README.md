#gava Objective-C Coding Style Guide

 이 스타일 가이드는 개인적으로 iOS 플랫폼의 프로젝트를 진행할 때 길라잡이로 쓰기 위해 작성 중인 가이드입니다. 이 가이드는 [애플의 코코아 코딩 가이드라인](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/CodingGuidelines/CodingGuidelines.html)에 의거하여 작성되었으며, [NYTimes Objective-C Style Guide](https://github.com/NYTimes/objective-c-style-guide) 등 다른 가이드라인들을 참고하였습니다.

## 목차
* [기본 원칙](#기본-원칙)
	* [가독성을 최우선으로](#가독성을-최우선으로)
	* [최대한 자연어에 가깝게](#최대한-자연어에-가깝게)
	* [축약어를 최대한 배제](#축약어를-최대한-배제)
* [띄어쓰기](#띄어쓰기)
    * [탭 대신 네 칸의 공백으로](#탭-대신-네-칸의-공백으로)
    * [메소드 공백](#메소드-공백)
    * [프로퍼티 공백](#프로퍼티-공백)
    * [if/else, switch/case, for, while](#if/else,-switch/case,-for,-while)
    * [클래스 / 프로토콜 헤더 정의 시](#클래스-/-프로토콜-헤더-정의-시)
* [코드의 순서](#코드의-순서)
    * [헤더파일 내용의 기본적인 순서](#헤더파일-내용의-기본적인-순서)
    * [구현파일 내용의 기본적인 순서](#구현파일-내용의-기본적인-순서)
    * [UIViewController SubClasses](#UIViewController-SubClasses)
* [파트 별 설명](#파트-별-설명)
* [단축표현법](#단축표현법)
* [파일 확장자](#파일-확장자)
* [Class Prefix](#Class-Prefix)
* [Define Preprocessor](#Define-Preprocessor)
* [매크로 네이밍](#매크로-네이밍)
* [변수 네이밍](#변수-네이밍)
* [메소드 네이밍](#메소드-네이밍)
    * [Accesor Methods](#Accesor-Methods)
    * [델리게이트 메소드](#델리게이트-메소드)
    * [파라미터 이름](#파라미터-이름)
* [데이터 타입](#데이터-타입)
    * [BOOL](#BOOL)
    * [Some Primitive Types](#Some-Primitive-Types)
    * [Enums](#Enums)
    * [Notification](#Notification)
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

 **Good:**
 ```objc
 UITextField *nameTextField;
 WriteViewController *writeViewController;
 - (void)invokeMethod:(selector)aMethod;
 ```
 **Bad:**
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

 **SEE ALSO:**
 * [Coding Guidelines for Cocoa - Code Naming Basics](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/CodingGuidelines/Articles/NamingBasics.html)
 * 예외의 예시는 [Coding Guidelines for Cocoa - Acceptable Abbreviations and Acronyms](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/CodingGuidelines/Articles/APIAbbreviations.html)를 참고 바랍니다.


## 띄어쓰기

* #####탭 대신 네 칸의 공백으로

 Xcode의 `Preferences` 메뉴에서 `Text Editing` -> `Indentation` 탭을 선택하면 Tab 키를 누를 때의 동작을 선택할 수 있습니다. *Indent in leading whitespace*가 기본값이므로, 기본값 상태에서 Tab 키를 누르면 자동으로 탭 문자 대신 스페이스 4칸이 들어갑니다.

* #####메소드 공백
 - **클래스 지정자(`-`/`+`) 뒤에는 Space 한 칸이 붙습니다.**

    **Good:**

	```objc
	- (void)methodName:(NSString *)nameString
	```

    **Not Good:**

	```objc
	-(void)methodName:(NSString *)nameString
	```

 - **반환 타입(```BOOL```, ```NSObject``` 등) 뒤에는 Space가 붙지 않습니다.**

    **Good:**

	```objc
	- (void)methodName:(NSString *)nameString
	```

    **Not Good:**

	```objc
	-(void)methodName:(NSString *)nameString
	```

 - **`메소드 이름`과 `첫 파라미터의 타입`, 그리고 `파라미터 이름` 앞에는 Space가 붙지 않습니다. **

    **Good:**

	```objc
	- (void)methodName:(NSString *)nameString
	```

	**Not Good:**

	```objc
	- (void)methodName: (NSString *)nameString
	```

	**Not Good:**

	```objc
	- (void)methodName:(NSString *) nameString
	```

 - **메소드 파라미터들 사이에는 Space 한 칸을 띄워줍니다.** 

    **Recommended:**

	```objc
	- (void)methodName:(NSString *)nameString infoArray:(NSArray *)infoArray
	```

   파라미터 이름이 너무 길거나 파라미터 개수가 3개 이상이라 가독성에 지장을 줄 가능성이 높은 경우에는 파라미터들을 개행으로 구분하는 것을 권장합니다.

	**Recommended:**

	```objc
	- (void)methodWithString:(NSString *)aNameString
				informations:(NSDictionary *)informations
				        flag:(bool)flag
	{
		return;
	}
	```

	이 점은 메세지를 보낼 때(메소드를 사용할 때)에도 마찬가지입니다.

	**Recommended:**

	```objc
	[object methodWithString:myName
				informations:informations
				        flag:YES];
	```

 - **메소드 블라켓의 시작`{`은 메소드 선언 바로 아래줄에 들어갑니다.**

	**Good:**

	```objc
	- (void)methodName:(NSString *)nameString
	{
		return;
	}
	```

	**Not Good:**

	```objc
	- (void)methodName:(NSString *)nameString {
		return;
	}
	```

	파라미터들을 개행으로 구분했다면, 블라켓은 반드시 다음 줄에서 시작해야 합니다.

	**Bad:**

	```objc
	- (void)methodWithString:(NSString *)nameString
				   infoArray:(NSArray *)infoArray
				        flag:(bool)flag {
		return;
	}
	```

  - **블라켓의 끝`}`은 메소드가 끝나는 바로 아래에 위치합니다.**

	**Good:**

	```objc
	- (void)methodName:(NSString *)nameString
	{
		return;
	}
	```

	**Bad:**

	```objc
	- (void)methodName:(NSString *)nameString
	{
		return; }
	```

 - **메소드 사이에는 개행 2줄을 띄웁니다.**

   이는 메소드와 메소드 사이의 구분을 좀 더 쉽게 하기 위함입니다.

	**Good:**

    ```objc
    - (id)alloc
	{
		id object;
		return object;
	}
//(blank)
//(blank)
	- (void)dealloc
	{
		return;
	}
	```

    **Not Good:**

	```objc
	- (id)alloc
	{
		id object;
		return object;
	}

	- (void)dealloc
	{
		return;
	}
	```

    **Bad:**

	```objc
	- (id)alloc
	{
		id object;
		return object;
	}
	- (void)dealloc
	{
		return;
	}
	```

* #####프로퍼티 공백

     **기본적인 문법:**

	```objc
	@property (nonatomic, getter=isEditable) BOOL editable;
	```

     **Not Good:**

	```objc
	// @property와 옵션들을 지정하는 블라켓()이 붙어있음
	@property(assign, getter=isEditable) BOOL editable;

	// () 안에서 ,로 구분되는 옵션들이 서로 붙어있음
	@property (assign,getter=isEditable) BOOL editable;

	// ()과 타입지정자가 붙어있음
	@property (assign, getter=isEditable)BOOL editable;

	```

* ##### if/else, switch/case, for, while

 - 여는 블라켓`{`은 개행하지 않고 inline으로 처리합니다.
 - 처리문의 시작은 블라켓 다음 줄부터 시작합니다.
 - 닫는 블라켓 `}`은 마지막 처리문 다음 줄에 넣고, else 등이 있으면 else 등을 `}` 바로 옆에 붙입니다.
 - 블라켓`{}` 처리 방식이 메소드의 블라켓 처리방식(*여는 블라켓을 다음 줄에 위치*)과 다르므로, 익숙해지면 둘 사이를 구분할 수 있게 되어 가독성에 도움을 줍니다.

   **Example: if/else**

	```objc
	if (!flag) {
    	// stuffs
	} else if (!exist) {
    	// other stuffs
	} else {
		// final stuffs
	}
	```

 - switch/case 문에서, case문 바로 뒤에 블라켓을 엽니다.

   **Example: switch/case**

	```objc
	switch (amount) {
		case 1: {
			// do stuffs
			break;
		}
		case 2: {
			// other stuffs
			break;
		}
		case 3:
		case 4: {
			// epic stuffs
			break;
		}
		default: {
			break;
		}
	}
	```

 - for와 while 문에서는 연산자 사이를 모두 띄어쓰는 것을 권장합니다.

	**Example: for**

	```objc
	for (NSInteger i = 0; i < 10; i++) {
		// do stuffs
	}
	```
	```objc
	for (NSObject *object in objects) {
		// do stuffs
	}
	```

	**Example: while**

	```objc
	while (playedCount < UINT64_MAX) {
		// play Lotto
	}
	```

* ##### 클래스 / 프로토콜 헤더 정의 시
 - `@class` 선언은 한 줄에 나열하며, `,` 뒤에 한 칸을 띕니다.
 - 모든 `@~`선언은 앞뒤에 한 줄씩 비웁니다.
 - 프로퍼티, 메소드들 사이에는 카테고리를 구분하기 위해서만 빈 줄을 한 줄 넣습니다.
 - 주석은 설명하고자 하는 라인 바로 위에 달고, 주석과 대상 사이에 빈 줄을 넣지 않습니다.
    **Example**:
	```objc
	@import Foundation;
    #import "Currency.h"
	#import "Wallet.h"

	@class MoneyClip, Bill, CreditCard, CheckCard, IDCard, Lotto;

	@protocol MoneyClipDelegate <NSObject>

	@Optional

    - (void)MoneyClip:(MoneyClip *)moneyClip willSpendBillWithAmount:(NSUInteger)spendAmount
                                                          ofCurrency:(Currency)*currency;
	- (void)MoneyClip:(MoneyClip *)moneyClip didSpendBillWithAmount:(NSUInteger)spendAmount
                                                         ofCurrency:(Currency)*currency;

	@end

	@interface MoneyClip : Wallet <NSURLConnectionDelegate> {
		...
	}

	//
	@property (nonatomic, strong) NSMutableArray *bills;
	@property (nonatomic, strong) NSMutableArray *cards;

	@property (nonatomic, readOnly) NSUInteger cardPocketAmount;

	/* 신용카드로 로또를 삽니다
     * @param card: 카드
	 */
	- (Lotto *)spendCreditCardOnLotto:(CreditCard *)card;

	@end

	```

## 코드의 순서
* ##### 헤더파일 내용의 기본적인 순서
  1. 클래스/파일에 대한 설명 (주석)
	- Xcode가 자동적으로 생성하는 주석을 의도에 맞게 내용만 바꾸는 걸로도 충분합니다.
	- 추가적으로 설명할 사항(라이센스 등)이 있으면, 바로 뒤에 기술합니다.
  2. `#import`들
	- `@import` (Framework Module)을 제일 먼저 기술합니다.
	- `#include`와 `#import`할 파일들을 기술합니다.
	- `#include`보다는 `#import`를 권장하는데, 이는 `#import`가 Header Guard를 하지 않아도 되는 편의성을 제공하기 때문입니다.
	- **선언에만 필요한 클래스 선언은 `#import`로 하지 않고 `@class`로 합니다. 바로 아래 항목을 참고 바랍니다.**
	 ```objc
     @import Foundation;
     @import CoreData;
     @import UIKit;
     #import "EXReferenced.h"
     #import "TTTAttributedLabel.h"
     ```
  3. `@class` 선언
	- `@class` 선언은 해당 헤더를 통째로 읽어들이는 `#import`와 달리, 포인터에 불과합니다.
	- `#import`를 통해서 헤더를 읽어야 하는 클래스는
		- 해당 클래스의 *Super Class*
		- 해당 클래스가 기술하거나 참조해야 하는 *프로토콜*

		정도이며, 나머지 선언을 위한 클래스 지정은 `@class`로 충분합니다.
    - `@class`로 선언된 변수/인스턴스를 구현부`.m`에서 쓰려면, `.m`에서 `#import`를 사용하여 헤더를 읽어야 합니다.
     **(.h)**

      ```objc
      @class CCScreenLayout, CCVideoUtility, CCImageProcess;
      ```

      **(.m)**
      ```objc
      #import "CCScreenLayout.h"
      #import "CCVideoUtility.h"
      #import "CCImageProcess.h"
      ```

	**SEE ALSO:**
	 * `@class` 사용의 이점은 컴파일/링크 시점에서 도드라집니다. 이에 대한 [Apple의 설명](https://developer.apple.com/legacy/library/documentation/Cocoa/Conceptual/OOPandObjC1/OOPandObjC1.pdf)이 있습니다. 해당 링크의 31페이지를 참조 바랍니다.

  4. 상수들

   **(.h)**
	```objc
	extern NSString const * CCsomethingConstant;
    ```
   **(.m)**
    ```objc
	NSString const* CCStringConst = @"constant";
	```
  5. typedef로 정의하는 타입들

		```objc
	typedef NSUInteger Dollar;
	typedef NS_ENUM (NSInteger, SpendType) {
		SpendTypeBill,
		SpendTypeCreditCard,
		SpendTypeDebitCard,
	};
	```

  6. @protocol 정의
	- 해당 클래스에서 사용할 프로토콜을 정의하고자 한다면, 프로토콜 정의가 클래스 정의보다 더 일찍 나오는 것이 클래식한 C 스타일에 부합합니다.
	- 프로토콜에서 해당 클래스를 사용하고자 한다면, @protocol이 나오기 전에 @class 문으로 해당 클래스를 미리 정의해야 합니다.

		```objc
		@class FooClass
		@protocol FooClassDelegate
		- (void)FooClassInstance:(FooClass *)instance didSomething:(bool)somethingDone
		@end
		```

  7. @interface 선언
   ```objc
   @interface FooClass : NSObject
   ```

  8. 프로퍼티 선언
   ```objc
   @property (nonatomic, assign, getter=isFoo) BOOL foo;
   ```
   - 바깥에서 접근해야 하는 변수들을 헤더에서 프로퍼티로 선언합니다.
   - 인스턴스 변수를 꼭 선언해야 한다면, 헤더(`.h`)가 아닌 구현부(`.m`)에서 @protected나 @private로 선언합니다.
   - **@public 인스턴스 변수는 절대 사용하지 않습니다.** (기본 상태는 @protected입니다.)

  9. 메소드 선언
   ```objc
   - (void)askCanYouBuildASnowMan;
   - (NSArray)fooSpaceShips;
   ```
  10. @end


* ##### 구현파일 내용의 기본적인 순서

 1. 클래스/파일에 대한 설명
 2. `#import`들
     ```objc
     #import "EXReferenced.h"
     #import "TTTAttributedLabel.h"
     ```
 3. const 상수 정의
     ```objc
     NSString * const CCsomethingConstant = @"com.ccushi.exam.constant.something";
     ```
 4. Private Interface(property, method 등)을 빈 카테고리에 선언
    * 프로퍼티
      * 클래스 내부변수들도 프로퍼티로서 정의합니다.

        **DO**
        ```objc
        @interface MainViewController ()

        @property (nonatomic) NSUInteger barrelMinAmount;
        @property (nonatomic) NSUInteger barrelMaxAmount;
        @property (nonatomic) NSUInteger currentBarrelAmount;

        - (BOOL)checkUserAccount;

        @end

        @implementation MainViewController
        .
        .
        .
        ```
      * 기존 방법의 인스턴스 변수 선언은 하지 않습니다.

        **DO NOT**
        ```objc
        @interface MainViewController ()
        {
        	NSUInteger barrentMinAmount;
        	NSUInteger barrentMaxAmount;
            NSUInteger currentBarrelAmount;
        }
        @end

        @implementation MainViewController
        .
        .
        .
        ```
 5. @implementation

    ```objc
    @implementation MainViewController
    ```
 6. Method 구현
 7. @end


* ##### UIViewController SubClasses

 1. NSObject 멤버 메소드의 오버라이딩을 가장 위에 배치합니다.
    - `- (id)init`, `- (void)dealloc` 등
 2. 그 다음에는 UIViewController Lifecycle을 배치합니다.
    - `- (void)viewDidLoad`, `- (void)viewDidDisappear` 등을 배치합니다.
 3. Framework Protocol Delegate들의 메소드들
 4. Custom Protocol Delegate들의 메소드들
 5. Public Methods
 6. Private Methods


## 파트 별 설명

- 한 클래스 내의 메소드들을 일정한 카테고리들로 묶을 수 있다면, 해당되는 메소드들을 최대한 가까이 모으고 메소드들의 바로 위에
	```objc
    #pragma mark - 파트에 대한 설명
    ```
	을 달아줍니다.

- 헤더`.h`와 구현부`.m`에 모두 달아주는 것을 권장합니다.


## 단축표현법

 Modern Objective-C Literals는 Apple LLVM Compiler 4.0부터 지원하기 시작한 Objective-C의 새로운 문법입니다. NSNumber와 NSArray, NSDictionary 등의 문법을 `@`로 시작하는 표현들과 JSON 스타일의 `[]`, `{:}` 등을 이용하는 문법으로 대체함으로써, 작성할 때와 읽을 때 모두 획기적으로 간결해졌다는 것이 특징입니다.

* ##### NSNumber
 - Old

	```objc
	NSNumber *fortyTwo = [NSNumber numberWithInt: 42];
	NSNumber *fortyTwoUnsigned = [NSNumber numberWithUnsignedInt: 42U];
	NSNumber *fortyTwoLong = [NSNumber numberWithLong: 42L];
	NSNumber *fortyTwoLongLong = [NSNumber numberWithLongLong: 42LL];

	NSNumber *piFloat = [NSNumber numberWithFloat:3.141592654F];
	NSNumber *piDouble = [NSNumber numberWithDoule:3.1415926535];

	NSNumber *yesNumber = [NSNumber numberWithBool:YES];
	NSNumber *noNumber = [NSNumber numberWithBool:NO];
	```

 - New *(Recommended)*

	```objc
	NSNumber *fortyTwo = @42;
	NSNumber *fortyTwoUnsigned = @42U;
	NSNumber *fortyTwoLong = @42L;
	NSNumber *fortyTwoLongLong = @42LL;

	NSNumber *piFloat = @3.141592654F;
	NSNumber *piDouble = [NSNumber numberWithDoule:3.1415926535];

	NSNumber *yesNumber = [NSNumber numberWithBool:YES];
	NSNumber *noNumber = [NSNumber numberWithBool:NO];
	```

* ##### NSArray
 - Old

	```objc
	NSArray *alphabets = [NSArray arrayWithObject: a, b, c, nil];
	id bb = [alphabets objectAtIndex:1];
	```

 - New *(Recommended)*

	```objc
	NSArray *alphabets = @[a, b, c];
	id bb = alphabets[1];
	```

* ##### NSDictionary
 - Old

	```objc
	NSDictionary *dict = [NSDictionary dictionaryWithObjectAndKeys:key1, value1, key2, value2, nil];
	id value11 = [dict objectForKey:key1];
	```

 - New *(Recommended)*

	```objc
	NSDictionary *dict = @{key1:value1, key2:value2};
	id value22 = dict[key2];
	```


## 파일 확장자
  - Objective-C Class Header: `.h`
  - Objective-C Class Implementation: `.m`
  - Objective-C++ Class Implementation: `.mm`
  - Pure C Class Header: `.h`
  - Pure C Class Implementation: `.c`
  - Pure C++ Class Implementation: `.cc`


## Class Prefix

Prefix를 붙일 땐 기본적으로 두 가지 원칙에 따릅니다.

  - 다른 프로젝트에서도 쓸 수 있는 범용 클래스일 경우 `CCushi`를 줄인 `CC`를 사용
  - 해당 프로젝트에서만 쓰이는 클래스일 경우, 해당 프로젝트명을 2~3글자의 영문자로 줄인 축약어를 사용
	- 프랜즈파크(`F`riends`P`ark) -> `FP`MainViewController
	- 추모의전당(`M`emorial`N`etwork) -> `MN`MainScrollView
	* *노마드샵(`N`omad`S`hop)의 경우에는 Apple의 프레임워크 prefix인 `NS`(NextStep)과 겹치기 때문에, `NMS`(NoMadShop) 등 **다른 대안을 찾아 붙입니다.** `UI`, `CG` 등과 겹치는 경우도 마찬가지입니다.*

  Xcode에서는 프로젝트 생성 시 Class prefix를 지정할 수 있습니다. 물론 생성 후에도 변경 가능합니다. 프로젝트용 prefix를 지정하면 프로젝트 진행 중 새로운 클래스를 행성할 때마다 이름 란에 prefix가 기본적으로 붙어서 나오기 때문에 편합니다.


## Define Preprocessor
일반적으로 #define 전처리기는 상수를 정의할 때는 쓰지 않습니다.

**DO:**
```objc
static NSString * const NMSServiceDomain = @"https://nomadshop.biz";
static const NSUInteger NMSMainViewControllerShopNameMaxLine = 3;
```
**DO NOT:**
```objc
#define NomadShopServiceDomain @"https://nomadshpo.biz"
#define ShopNameMaxLine 3
```


## 매크로 네이밍

- 매크로의 이름을 정의할 때는
  - 모두 대문자 UPPERCASE로 합니다.

    **Good:**
    ```objc
    #define CC_STRONG
    ```
    **Not Good:**
    ```objc
    #define CCStrong
    ```
  - 단어의 사이는 underscore`_`로 연결합니다.
  - [Class Prefix](#Class-Prefix)와 같은 규칙을 적용하여 Prefix를 붙입니다. Prefix와 다음 단어들과는 underscore`_`로 연결합니다. 이는 위 항목의 방식과 동일합니다.

    ```objc
    #ifndef CC_STRONG
    #if __has_feature(objc_arc)
    #define CC_STRONG strong
    #else
    #define CC_STRONG retain
    #endif
    #endif
    ```

## 변수 네이밍

> Long, descriptive method and variable names are good.
>
> [NYT Objective-C Style Guide](https://github.com/NYTimes/objective-c-style-guide#naming)

모든 네이밍은 단어를 축약하지 않고 온전히 사용하는 것을 권장합니다. 이는 아래 나올 메소드 네이밍에서도 같지만, 변수에서 특히 요구됩니다.

* [헝가리안 노테이션 Hungarian Notation](http://msdn.microsoft.com/en-us/library/aa378932%28VS.85%29.aspx)스타일의 Prefix를 쓰지 않습니다.

    **DO:**
    ```objc
    int amount;
    ```
    **DO NOT:**
    ```objc
    int iAmount;
    ```
   현재 Xcode에서는 Code assist나 (⌘+왼클릭) 등으로 쉽게 변수의 타입을 알아볼 수 있습니다. 타입을 알리기 위해 굳이 축약된 기호를 prefix에 붙일 필요가 없습니다.

* 타입을 명시해야 할 필요가 있는 변수에는 변수명 끝에 클래스 이름을 붙입니다. 이 때 클래스의 Prefix를 떼고 붙입니다.

    **Good:**
    ```objc
    NSArray *dockArray;
    NSDictionary *metadataDictionary;
    NSInteger priceIntegerValue;

    UITextField *passwordTextField;
    UIImageView *birdImageView;
    ```
    **Bad:**
    ```objc
    NSArray *arrDock;
    NSArray *dockArr;
    NSArray *dockNSArray;
    NSArray *dicMetadata;
    NSArray *MetadataNSDictionary;
    NSInteger iPrice;

    UITextField *pwTF;
    UIImageView *birdIV;
    ```


## 메소드 네이밍
Apple에서는 [메소드 이름 짓는 법](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/CodingGuidelines/Articles/NamingMethods.html)을 상세하게 기술하고 있습니다.

* 메소드의 이름은 소문자로 시작하고 CamelCase를 씁니다. Prefix는 사용하지 않습니다.

	```objc
	fontFromLabel: // Good
	CCFontFromLabel: // bad
	```

* 특히, 맨 앞에 underscore`_`를 붙이지 않습니다. Cocoa Framework가 대부분의 private methods를 `_`로 시작하는 네이밍을 사용하기 때문에, 이는 사실상 애플의 예약어라고 생각하면 되겠습니다.

* 결과값을 돌려주는 게 목적인 메소드는 결과값의 이름을 메소드의 이름으로 합니다. `calc`, `get` 등은 불필요하므로 사용하지 않습니다.

	```objc
	- (NSInteger)score // good
	- (NSInteger)getScore // bad
	- (NSInteger)calcScore // bad
	```

* 리턴값 없이 어떤 동작을 하는 것을 목표로 하는 메소드는 그 동작을 동사verb로 기술합니다. 동작에 필요한 재료가 파라미터로 있다면, 파라미터의 설명을 첫 파라미터가 나오기 전에 기술해야 합니다.

	```objc
	- (NSInteger)arrangeLayoutInRect:(CGRect)rect // Good
	- (NSInteger)arrangeLayout:(CGRect)rect // Bad
	```

- 모든 파라미터들은 `:` 앞에 파라미터의 설명이 있어야 합니다.

	```objc
	- (void)sendAction:(SEL)aSelector toObject:(id)anObject forAllCells:(BOOL)flag; // 	Good.
	- (void)sendAction:(SEL)aSelector :(id)anObject :(BOOL)flag; // Terrible.
	```

- `Do`나 `Does`는 `Will`이나 `Can`와 달리 메소드의 의미를 명확히 하는 데 도움이 되지 않습니다. 따라서 `Do`나 `Does`는 메소드 이름에 쓰지 않습니다. 이는 애플의 가이드라인에 반복적으로 등장합니다.


### Accesor Methods
- 프로퍼티 @property를 지정하면 LLVM 컴파일러가 자동으로 지정자를 생성합니다.

	```objc
	/* 프로퍼티 */
	@property (nonatomic) BOOL suspended;

	// 자동으로 생성되는 Getter
	- (BOOL)suspended

	// 자동으로 생성되는 Setter
	- (void)setSuspended:(BOOL)aSuspended
	```

- 하지만 bool 타입의 프로퍼티의 경우에는 많은 가이드라인들이 Getter에 `is` Prefix를 붙이는 것을 권장합니다. 이유는 역시 사용할 때 자연어에 가깝기 때문입니다.

	```objc
	BOOL flag;
	flag = [self suspended]; // suspend된 상태 여부를 원하는 건지 suspend를 시행한 결과를 원하는 건지 불분명함
	flag = [self isSuspended]; // suspend된 상태 여부를 원하는 것임이 분명함
	```

	**Getter를 지정하는 예시:**

	```objc
	@property (nonatomic, readonly, getter=isSuspended) BOOL suspended;
	```

- Setter는 일반적인 LLVM 4.0 이상의 Compiler로 컴파일 시 자동으로 생성되는 이름에 무리가 없기 때문에, 별다른 이름을 써서 선언하지 않는 것을 권장합니다.


### 델리게이트 메소드
델리깃(델리게이트) 메소드 Delegate Methods의 명명법은 [애플의 가이드라인](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/CodingGuidelines/Articles/NamingMethods.html#//apple_ref/doc/uid/20001282-1001803-BCIDAIJE)을 그대로 따릅니다.

- 메소드의 이름은 메소드를 보내는 클래스의 이름부터 시작합니다.

	```objc
	- (BOOL)tableView:(NSTableView *)tableView shouldSelectRow:(NSInteger)row;
	- (BOOL)application:(NSApplication *)sender openFile:(NSString *)filename;
	```
	메소드의 이름에서 Prefix를 빼며, 다른 메소드들과 같이 소문자로 시작합니다.

- 메소드를 보내는 클래스 인스턴스 외에 특별히 들어갈 파라미터가 없다면, 첫 번째 콜론`:`은 클래스 이름과 동작을 모두 기술한 후 붙입니다.

	```objc
	- (BOOL)ApplicationOpenUntitledFile:(NSApplication *)sender;
	```

	형식: [+|-] (BOOL)[클래스 이름]`Application`[동작]`OpenUntitledFile`[콜론]`:`[클래스 인스턴스]`(NSApplication *)sender`;

- Notification을 보내는 메소드는 예외로 합니다. 아래 예와 같이, Notification 객체를 보내는 메소드는 클래스를 생략하고 Notification 객체만을 파라미터로 합니다.

	```objc
	- (void)windowDidChangeScreen:(NSNotifcation *)notification;
	```

- **did**, **will**, **should**
	- *did*와 *will*은 어떤 일이 일어났거나, 일어나려고 할 때 델리깃의 동작을 정의하기 위해 사용합니다.

		```objc
		- (void)browserDidScroll:(NSBrowser *)sender; // 브라우저가 스크롤할 때마다 호출됨
		- (NSUndoManager *)windowWillReturnUndoManager:(NSWindow *)window; // 윈도우가 UndoManager를 돌려주기 직전에 호출됨
		```
	- *should*는 어떤 동작을 할지 말지의 여부를 델리깃에게 물어보기 위해 사용합니다. 델리깃은 결과값을 알려주기 전에 메소드 안에서 여러 작업을 처리할 수 있습니다.

		```objc
		- (BOOL)windowShouldClose:(id)sender; // 윈도우가 닫힐지 여부를 델리깃에 물어봅니다.
		```

### 파라미터 이름
애플에서는 몇 가지 일반적인 룰을 정해놓고 있습니다.
- 소문자로 시작하며, CamelCase를 사용합니다.
- `pointer`나 `ptr`를 쓰지 않습니다. 파라미터가 포인터인지 아닌지는 파라미터의 타입으로 표현하면 충분합니다.
- 1~2글자로 명명하지 않습니다.
- 축약어를 사용하지 않습니다. 그래봤자 몇 글자 못 절약합니다. 자연스럽게 읽히는 것이 우선입니다.
애플에서 쓰는 파라미터의 예입니다.

	```objc
	...action:(SEL)aSelector
	...alignment:(int)mode
	...atIndex:(int)index
	...content:(NSRect)aRect
	...doubleValue:(double)aDouble
	...floatValue:(float)aFloat
	...font:(NSFont *)fontObj
	...frame:(NSRect)frameRect
	...intValue:(int)anInt
	...keyEquivalent:(NSString *)charCode
	...length:(int)numBytes
	...point:(NSPoint)aPoint
	...stringValue:(NSString *)aString
	...tag:(int)anInt
	...target:(id)anObject
	...title:(NSString *)aString

	```



## 데이터 타입

### BOOL
- 타입 선언은 `BOOL`을 권장합니다.
- 타 언어/플랫폼과의 이식성을 중요시한다면 `bool`을 권장합니다.

LLVM 4.0 컴파일러에서 하이라이팅되는 boolean 타입은

    - 일반적으로 쓰이는 C99 타입의 native `bool`과 `_Bool`
    - Objc.h에 정의된 `BOOL`
    - MacTypes.h에 정의된 `Boolean`
    - boolean.h에 정의된 `boolean_t`

등이 있습니다.

이들 중 소문자로 시작하는 camelCase의 변수명과 쉽게 구분되는 대문자 `BOOL`을 권장합니다.
다만, 이식성을 중요시한다면 C99 Native 타입인 `bool`을 권장합니다.

같은 이유로, Objective-C 스타일의 `YES / NO`, C 스타일의 `true / false` 사이에서도 같은 방법의 선택을 권장합니다.


### Some Primitive Types

- int보다는 NSInteger를 권장합니다.
- 다만 고정된 int 크기의 타입을 요할 시 int를 사용합니다.

64-bit 기반으로 컴파일할 시, NSInteger가 long으로 변환되어 컴파일되는 것과 달리, int는 단순히 int로 컴파일됩니다. 64-bit에 유연하게 대응되는 시스템을 지향한다면 NSInteger를 더 권장합니다.

[애플의 설명](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/Cocoa64BitGuide/64BitChangesCocoa/64BitChangesCocoa.html#//apple_ref/doc/uid/TP40004247-CH4-SW11)과 `NSObjCRuntime.h`을 참조 바랍니다.

같은 이유로,

- *float*보다는 *CGFloat*를 권장합니다.
- 다만 고정된 *float* 크기의 타입을 요할 시 *float*를 사용합니다.

특히, CoreGraphics에서 쓰이는 구조체들(*CGRect*, *CGPoint*, *CGSize*, *CGVector* 등)은 이미 *float*가 아닌 CGFloat 타입의 변수들을 멤버로 정의하고 있습니다. `CGGeometry.h`를 참조 바랍니다.
그렇기 때문에, *UIView*의 *bounds*, *frame*에 들어갈 값을 저장하는 변수라면 특히나 **`float`보다 `CGFloat`를 권장합니다**.


### Enums
- enum 타입은 전통적인 typedef enum 문법이 아닌 typedef NS_ENUM 매크로를 사용할 것을 추천합니다.
앞서 언급한 int, float와 비슷한 이유인데, 기존의 `typedef enum`으로만 선언하게 되면, [상황에 따라 enum 타입의 크기가 달라질 수 있기 때문입니다](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/Cocoa64BitGuide/64BitChangesCocoa/64BitChangesCocoa.html#//apple_ref/doc/uid/TP40004247-CH4-SW8).

	```objc
	typedef enum {
		CCProjectTypeOurGame,
		CCProjectTypeOurApp,
		CCProjectTypeOthersApp,
	} CCProjectType; // unsigned int인지 long인지 확실하지 않음
	```

	결국 좀 더 정확한 사용을 위해서는

	```objc
	typedef enum CCProjectType : NSInteger
	{
	    CCProjectTypeOurGame,
	    CCProjectTypeOurApp,
    	CCProjectTypeOthersApp,
	} CCProjectType;
	```

	혹은

	```objc
	enum {
		CCProjectTypeOurGame,
		CCProjectTypeOurApp,
		CCProjectTypeOthersApp,
	} CCProjectType;
	typedef NSUInteger CCProjectType;
	```

	과 같이 처리해야 하는데, 애플은 이에 대응하여

	```objc
	typedef NS_ENUM(NSUInteger, CCProjectType) {
		CCProjectTypeOurGame,
		CCProjectTypeOurApp,
		CCProjectTypeOthersApp,
	};
	```

	과 같이 쓸 수 있는 매크로를 iOS 6 / OS X 10.8을 발표하면서 추가하였습니다.
	첫 줄에 enum의 타입명과 실제 타입이 명시되기 때문에, 코딩의 편의성과 가독성을 모두 잡는 방법입니다.


- 타입의 형식은

  ```objc
  [Class Prefix]+[TypeName]
  ```
으로,

- 값의 형식은

  ```objc
  [Class Prefix]+[TypeName]+[ValueName]
  ```
으로 합니다.

 **Example:**
  ```objc
  NS_ENUM (NSInteger, CCSpendType) { 
      CCSpendTypeBill,
      CCSpendTypeCreditCard,
      CCSpendTypeDebitCard,
  };
  ```


### Notification

Notification은 전역 NSString 상수로 정의합니다.

**(in .h)**

```objc
extern NSString * const NMSProductDidAddNotification;
```

**(in .m)**

```objc
NSString * const NMSProductDidAddNotification = @"com.nomadstar.nomadshop.product.added";
```


애플에서는 [Notification의 이름을 정하는 규칙](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/CodingGuidelines/Articles/NamingIvarsAndTypes.html)을 다음과 같이 정의했습니다. 

```objc
[Name of associated class] + [Did | Will] + [UniquePartOfName] + Notification
```


**Example:**

[Name of associated class]`NMSProduct`
[Did | Will]`Did`
[UniquePartofName]`Add`
[Notification]`Notification`


Notification의 내부 값은 Reverse domain name notation을 따릅니다.
글자들은 모두 소문자lowercase로 표기합니다.

**규칙:**
```objc
com.[ccushi | (Client's name)].[ProjectName].[Name of associated class].[UniquePartOfName]
```

**Example:**
```objc
NSString * const AODSailDataParserDidParseNotification = @"com.ccushi.aod.saildataparser.completeparsing";
```


## 같이 보기
[Coding Guidelines for Cocoa](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/CodingGuidelines/CodingGuidelines.html)

[NYTimes Objective-C Style Guide](https://github.com/NYTimes/objective-c-style-guide)

[Clean, Modern Objective-C by Harlan Haskins](https://harlanhaskins.com/2014/02/20/clean-modern-objective-c.html)