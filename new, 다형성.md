// 다형성   부모 클래스에서 상속 받은 함수와 이름은 같지만 완전히 다른 함수를 정의하고 싶으면 new를 써주면 됨. 

    // new (다형성 X)
    class Player
    {
        public int hp;
        public int attack;

        public void Move()
        {
            Console.Write("Player Move");
        }
    }

    class Knight : Player
    {
        public new void Move()
        {
            Console.Write("Knight Move");
        }
    }

    Knight knight = new Knight();
    knight.Move();    // Knight Move가 출력된다.
    
    
    // 다형성 (가상함수와 오버라이드)
    // 상속하는 함수라도 부모변수로 자식객체를 참조할 때(업케스팅) 자식들마다 실행 내용을 다르게 호출하고 싶을 때.

    class Player
    {
        public int hp;
        public int attack;

        public virtual void Move()
        {
            Console.Write("Player Move");
        }
    }

    class Knight : Player
    {
        public override void Move()
        {
            Console.Write("Knight Move");
        }
    }

    class Mage : Player
    {
        public override void Move()
        {
            Console.Write("Mage Move");
        }
    }

    int Test(Player player)
    {
        player.Move();
    }
    
    
    매개 변수인 player는 인수로 꼭 Player 객체 뿐 아니라 그 자식인 Knight와 Mage 타입 객체도 참조할 수 있음. player에 어떤 객체가 들어오냐에 따라 player.Move()를 다르게 실행하게
    하려면 1) Player에서 Move()를 가상함수로 선언하고 2)자식 클래스에서 이 함수를 override로 재정의함. 이게 다형성의 개념임.
    
    player.Move();
        Player.player = new Player();
        player의 Move 실행. Player Move 출력
        
        Player.player = new Knight();
        Knight의 Move 실행. Knight Move 출력
        
        Player.player = new Mage();
        Mage의 Move 실행. Mage Move 출력
        
    성능 문제 때문에 가상함수는 꼭 다형성이 필요할 때만 선언해주는 것이 좋음. 재정의하지 않고 그대로 상속받는게 성능상 가장 좋긴 함.
    
    
    만약 부모에서 가상함수는 선언했으나 자식에서 오버라이드 하지 않고 아래 코드와 같다면
    
    class Player
    {
        public int hp;
        public int attack;

        public virtual void Move()
        {
            Console.Write("Player Move");
        }
    }

    class Knight : Player
    {
        public void Move()
        {
            Console.Write("Knight Move");
        }
    }
    
    
    Player player = new Knight();
    player.Move();
    
    이 경우 Player.Move()를 실행해도 Knight 의 새로 정의 된 Move가 실행되지 않고 Player의 Move()가 실행된다. Knight의 Move()는 새로운 함수가 선언된 것이다. 오버라이드로 
    덮어씌운게 아니므로 Player의 원래 Move()함수가 나오는 것.
    
    
    class Player
    {
        public int hp;
        public int attack;

        public virtual void Move()
        {
            Console.Write("Player Move");
        }
    }

    class Knight : Player
    {
        public override void Move()
        {
            Console.Write("Knight Move");
        }
    }

    Player player = new Knight();
    player.Move();
    
    자식부분에서 override로 재정의해줘야 Player.Move()를 했을 때 Knight에서 재정의 한 Move 함수가 나온다.
    
    
    class Player
    {
        public int hp;
        public int attack;

        public virtual void Move()
        {
            Console.Write("Player Move");
        }
    }

    class Knight : Player
    {}

    class Mage : Player
    {
        public override void Move()
        {
            Console.Write("Mage Move");
        }
    }

    Player knightplayer = new Knight();
    Player mageplayer = new Mage();
    
    knightplayer.Move();   // 출력 Player Move
    mageplayer.Move();     // 출력 Mage Move
    
    //knight 플레이어는 재정의 해주는 부분이 없기 때문에 상속받은 부모 클래스의 Move 함수가 실행되어 "Player Move"가 출력된다.
    //반대로 mageplayer는 Mage 클래스에서 오버라이드 해주었기 때문에 갱신된 "Mage Move"가 출력된다.
    
    
    
    class Player
    {
        public int hp;
        public int attack;

        public virtual void Move()
        {
            Console.Write("Player Move");
        }
    }

    class Knight : Player
    {
        public override void Move()
        {
            base.Move();  // base로 부모 클래스에 접근. Player의 Move() 함수 추가함.
            Console.Write("Knight Move");
        }
    }

    Player player = new Knight();
    player.Move();
    
    // 결과 Player Move Knight Move
    
    base 키워드를 사용해 재정의 하는 대상인 부모 클래스의 가상함수를 사용하는 식으로 부모 함수의 기능을 일부 추가 가능함. Knight 클래스에서 오버라이드 할때 base.Move()로 
    부모 클래스의 Move() 함수를 추가하도록 설정했기 때문에 해당 기능이 추가 된 것임.
    
    
    
    //sealed
    //자식이 자기를 오버라이드 하는 것 까지만 허용하고 그 밑 손자 증손자가 부모 오버라이드 하는 것은 금지. 잘 쓰이는 기능은 아니라 함.
    
    class Player
    {
        public int hp;
        public int attack;

        public virtual void Move()
        {
            Console.Write("Player Move");
        }
    }

    class Knight : Player
    {
        public sealed override void Move()
        {
            Console.Write("Knight Move");
        }
    }

    class grandKnight : Knight
    {
        public override void Move()     // 위에서 seal로 묶었기 때문에 오버라이드 불가능.
        {
            Console.Write("grandKnight Move");
        }
    }
    
    // seal로 묶었을 땐 그 밑은 오버라이드 불가능. 그냥 상속 받아서 써야 한다.
