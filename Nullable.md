// Nullable
    // Nullable -> Null + able. 값이 없다는 것을 표현할 수 있도록 int 같이 null 값을 가질 수 없는 데이터들이 null 값을 가질 수 있도록 하는 것.
    // 객체를 참조하는 변수는 (Monster monster 같은) null을 가질 수 있다.
    //  그러나 int, struct 같은 기본 자료형 변수는 null을 가질 수 없기 때문에 C# 에서는 값이 없다는 것을 표현할 수 있도록
    // 이 같은 변수들이 null 값을 가질 수 있도록 해주는 문법이 있다. -> Nullable
    // 값이 없으면 return 0 혹은 return -1 이런식으로 많이 표현하는데 return null로 표현할 수 있다면 더 좋을 것이다.

    // Nullable 속성과 함수
    // 1. Value
    //      Nullable 변수의 값을 리턴
    //      기존 데이터이거나 null이거나!
    // 2. HasValue
    //      Nullable 변수의 값이 null이면 False, null이 아니면 True 리턴
    // 3. GetValueOrDefault()
    //      null이 아니면 즉 값이 있는 경우 할당된 값을 리턴하고
    //      null이면 기존 타입의 default 값 리턴. (int라면 0을 리턴할 것이다.)
    
    // Nullable 선언 -> ? 를 붙인다.
    int? number = null;     // OK
    number = 3;             // OK

    int a = number;     // 컴파일 에러 발생
    int b = number.Value;       // OK. But 런타임 에러 우려
    
    // number는 null값을 저장하는 것도 가능한 int형 변수가 되었다.
    int? number = null;
    
    // a는 Nullable 하지 않은 일반 int이므로 number를 받을 수 없다. (변환 불가)
    // number.Value값이 null이 아니라면 문제 없이 b에 할당 되지만, 만약 null이라면 이를 일반 int 변수인 b에서는 이를 할당 받을 수 없기 때문에 런타임 에러가 발생한다.
    
    // 따라서 null이라면, 아니라면 이런 if-else 문을 통한 체크가 필요하다
    // 첫번째 방법
    if (number != null)
    {
        
    }
    
    // 두번째 방법
    if (number.HasValue)    // null이 아니라면 True 리턴
    {
        
    }
    
    // 세번째 방법
    int b = number ?? 0;
    
    //
    Monster monster = null;
    if (monster != null)
        int monsterId = monster.Id;
    else
        int monsterID = 0;
    
    // 객체가 null인지 아닌지 체크하고 진행할 때가 많다. 위와 같이 할 수도 있지만
    int? id = monster?.Id;
    // 이렇게 한 줄로 끝낼 수 있다. monster?.Id; -> monster가 null이 아니면 monster.Id가 리턴되고, monster가 null이면 null이 리턴된다.
    
    
    //  ?? 문법
    int b = number ?? 0;        // (number가 null이면 0을 리턴, null이 아니면 그래도 number.value 리턴)
    int c = (number != null) ? number.Value : 0;
    // 위 두 줄의 코드는 같은 로직을 한다.
    // ??을 사용하면 A ?? B Nullable 변수인 A가 null이라면 0 을 리턴하고, null이 아니라면 그대로 number.Value값을 리턴한다는 의미이다.
