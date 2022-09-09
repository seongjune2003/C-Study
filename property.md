// Property
    // 외부에서 값을 바꾸면 그 값을 누가 언제 바꿨는지 알기가 쉽지 않음. 따라서 외부에서 write되지 않기를 원하는 멤버 함수는 protected, private으로 
    // 접근을 제한하고 setter, getter와 같은 접근 함수를 public으로 만들어서 이들에 대해 간접 접근한다.
    // (이런 경우 디버깅시 호출 스택을 통해 어디서 누가 호출했는지 쉽게 알 수 있다.)
    
    // 프로퍼티는 은닉성과 관련이 있으며 Getter와 Setter 접근 함수와 같은 기능을 좀 더 편하게 사용하기 위한 기능이다.
    // 그래서 사용법도 함수와 비슷하다.

    class Knight
    {
        protected int hp;
        
        // 프로퍼티
        public int Hp
        {
            get { return hp; }
            set { hp = value; }
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            Knight knight = new Knight();

            knight.Hp = 100;    // Set (value에 100이 들어감)
            int hp = knight.Hp;     // Get
        }
    }
    
    //이것이 프로퍼티의 정의다. set에서 value는 Write 하려는 새로운 값을 뜻한다.
    
    /*
    public int Hp
    {
        get { return hp; }
        set { hp = value; }
    }
    */
    
    //Knight 클래스의 멤버 프로퍼티 Hp 값을 가져올 땐 자동으로 get { return hp; }가 호출된다.
    int hp = knight.Hp;   // Hp 프로퍼티의 get 호출
    
    // Knight 클래스의 멤버 프로퍼티 Hp 값을 Write 할 땐 자동으로 set { hp = value; }가 호출된다
    knight.Hp = 100;    // Set   (value에 100이 들어간다.)
    
    
    // 이처럼 Getter, Setter 접근 함수와 같은 기능을 이렇게 프로퍼티 하나로 간단하게 구현할 수 있다.
    // 외부에서 사용될 수 없는 protected 제한자인 멤버 변수 hp는 Hp 프로퍼티의 get, set을 통해 간접 접근할 수 있게 된다.
    public int Hp
    {
        get { return hp; }
    }
    
    // 위와 같이 get, set 중에 하나만 정의해도 무방하다. 위와 같은 경우에 set은 정의하지 않았기 때문에 knight.Hp = 100;은 불가능하다.(컴파일 에러)
    // knight.Hp를 리턴받는 것만 가능하다.

    public int Hp
    {
        get { return hp; }
    }
    // 프로퍼티도 멤버이기 때문에 접근 제한자를 붙일 수 있다. 프로퍼티를 private로 제한하면 동일한 클래스 내부에서만 프로퍼티 사용이 가능하다.
    
    
    
    // 자동 구현 프로퍼티
    class Knight
    {
        public int Hp
        {
            get;
            set;
        }
    }
    
    // 프로퍼티를 위와 같이 구현하면 멤버 변수를 직접 만들어 줄 필요가 없다. 컴파일러가 private한 멤버 변수까지 자동으로 생성시켜주기 때문이다.
    // 간단하게 get; set; 만 써주면 자동 완성 프로퍼티다. 이렇게 정말 기본적인 Get, Set 작업만을 할 때 사용 가능하다. 
    // 뭔가 더 사용자 지정 코드를 작성할 경우에는 자동 완성 프로퍼티를 사용할 수 없다. 
    // get과 set에 {} 중괄호를 넣어 사용자 지정 코드를 구현하는 순간 더 이상 자동 완성 프로퍼티가 아니며 컴파일러는 자동으로 멤버 변수를 만들어 주지 않는다.
    
    
    private int _hp;

    public int GetHp()
    {
        return _hp;
    }

    public void SetHp(int value)
    {
        _hp = value;
    }
    
    // 자동 구현 프로퍼티는 위 코드 3 줄을 축약한 것과 동일하다. (멤버 변수 선언까지도 필요 없음. 자동으로 만들어주어서!)

    class Knight
    {
        public int Hp { get; set; } = 100;
    }

    // 더 나아가 이렇게 초기화도 가능하다. 아래 코드 3 줄과 같다.
    
    class Knight
    {
        public int _hp = 100;

        public int GetHp()
        {
            return _hp;
        }

        public void SetHp(int value)
        {
            _hp = value;
        }
    }
    
    
    // get, set 접근 지정자 다르게
    
    protected int Hp
    {
        get { return hp; }          // get 할 때는 Hp에 따라 protected. 이렇게 안써주면 프로퍼티 접근 지정자 따라간다.
        private set { hp = value; }  // set 할 때는 private
    }
    
