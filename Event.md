// delegate의 한계

    delegate int OnClicked();
    
    static void ButtonPressed(OnClicked clickedFunction)        // 델리게이트 그대로 받아옴
    {
        clickedFunction();
    }

    static void Main(string[] args)
    {
        OnClicked clicked = new OnClicked(Test);
        clicked += Test2;  // chaining
        clicked();
        
        ButtonPressed(clicked);

        clicked();
    }

    // 델리게이트 형식 OnClicked를 오직 ButtonPressed 함수 안에서만 실행시키기 위해 clickedFunction(); 만들었을 수도 있다.
    // 그러나 상관 없는, 그리고 외부인 메인 함수 안에서도 clicked(); 이렇게 델리게이트를 실행시킬 수 있다는 문제가 있다.


    // Event
    // event는 delegate와 달리 이벤트와 같은 클래스 안에서만 이벤트 호출이 가능하다.
    // 외부에선 오직 이벤트에 함수 등록만 해놓을 수 있으며 이벤트가 정의된 클래스 외부에서는 이벤트를 호출할 수는 없다. 이것이 델리게이트와의 차이점!
    
    // InputManager (같은 클래스)
    // 키보드 마우스 입력을 캐치해서 게임 로직에 이를 전달하는 역할로 정의한 클래스다.

    class InputManager
    {
        public delegate void OnInputKey();
        public event OnInputKey InputKey;   // public 접근 한정자까지 똑같이 맞춰야됨.

        public void Update()
        {
            if (Console.KeyAvailable == false)
                return;

            ConsoleKeyInfo info = Console.ReadKey();
            if (info.Key == ConsoleKey.A)   // A 키가 눌리면 이벤트 호출
            {
                InputKey();     // 구독자들에게 메세지 뿌리기 -> 옵저버 패턴
            }
        }
    }

    // Console.KeyAvailable  -> Key를 누를 수 있는 상태라면 True 리턴, Key를 사용할 수 없으면 False 리턴.
    // Console.ReadKey()    ->  사용자가 입력한 Key를 읽어들여 ConsoleKeyInfo 타입으로 리턴한다.
    
    // 이벤트 정의하기
    // 1. 먼저 delegate 형식부터 정의한다. (이벤트에 등록할 수 있는 함수 형식으로 쓸 것이다.)
    public delegate void OnInputKey();  // 매개 변수 없고 리턴 타입 없는 함수만 등록 가능한 형식
    
    // 2. 위에서 만든 delegate 형식을 가지는(= 타입이 해당 delegate인) 이벤트를 정의한다. 접근 한정자 + event + 델리게이트 이름 + 이벤트 이름
    public event OnInputKey InputKey;   // 이 이벤트의 타입은 OnInputKey 델리게이트
    // 델리게이트와 그 델리게이트를 타입으로 하여 정의한 이벤트는 둘 다 접근 한정자가 동일해야 한다. 둘 다 public으로 동일하여 문제 없음.
    
    // 사용자가 입력한 Key가 A라면 이벤트를 호출(실행)한다. 같은 클래스 내부에서 실행시키는 것이기 때문에 문제없다.
    //  InputManager 클래스 외부의 이곳 저곳에서 이 이벤트에 함수를 등록하고 이 이벤트에 등록된 함수가 무엇인지 알 필요없이 그저
    //  InputManager 클래스내에서 이를 실행만 하면 될 뿐이다.
    
    // 이와 같이 구독자(등록된 함수들)들에게 메시지를 뿌리는 디자인 패턴을 옵저버 패턴이라고 한다.
    // 옵저버 (https://glikmakesworld.tistory.com/3?category=797136)
    
    
    // Program (외부, 메인 함수 있음)
    class Program
    {
        static void OnInputTest()
        {
            Console.WriteLine("Input Received!");
        }

        static void Main(string[] args)
        {
            InputManager inputManager = new InputManager();
            InputManager.InputKey += OnInputTest;

            while (true)
            {
                inputManager.Update();
            }
            
            // inputManager.InputKey(); 컴파일 에러! 외부에서 호출 불가능
        }
    }

    
    // 이벤트를 사용하기 위해 InputManager 타입의 객체를 만들어 inputManager에서 이를 참조한다.
    // 이벤트에 OnInputTest() 함수를 등록한다.
    // inputManage.InputKey += OnInputTest;
    // 여기는 InputManager 클래스의 외부라서 이벤트를 직접 호출하는 것은 불가능하므로(inputManager.InputKey();는 컴파일 에러)
    // 이 이벤트를 호출하는 InputManager의 멤버 함수 inputManager.Update();를 실행시키면 된다!
    // 직접 이 안에서 입력이 들어오면 실행시킬 함수들을 구구절절 나열하고 직접 호출해줄 필요가 없이 inputManager.Update();만 실행시켜주면 땡이다!
    
    // 결론! 델리게이트와 이벤트는 기능은 동일하나 차이점은 👉 델리게이트와 달리 이벤트는 클래스 외부에서는 이벤트를 호출할 수는 없다는 것이다
