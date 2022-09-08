using System;
using System.Collections.Generic;
using System.Text;

namespace CsharpStudy
{
    // 플레이어 생성
    // Player.cs

    public enum PlayerType
    {
        None = 0,
        Knight = 1,
        Archer = 2,
        Mage = 3
    }

    class Player
    {
        protected int hp = 0;
        protected int attack = 0;
        protected PlayerType type = PlayerType.None;  // 디폴트

        protected Player(PlayerType type)
        {
            this.type = type;
        }

        public void SetInfo(int hp, int attack)
        {
            this.hp = hp;
            this.attack = attack;
        }

        public int GetHp()
        {
            return hp;
        }

        public int GetAttack()
        {
            return attack;
        }

        public PlayerType GetPlayerType()
        {
            return type;
        }
    }

    class Knight : Player
    {
        public Knight() : base(PlayerType.Knight)
        {
            SetInfo(100, 10);
        }
    }

    class Archer : Player
    {
        public Archer() : base(PlayerType.Archer)
        {
            SetInfo(75, 12);
        }
    }
    
    class Mage : Player
    {
        public Mage() : base(PlayerType.Mage)
        {
            SetInfo(50, 15);
        }
    }
    
    
부모인 Player 클래스는 단지 여러 직업의 공통적인 요소들을 모아두는 용도로 사용할 것이기 때문에 Player 타입의 객체는 외부에서 생성하지 못 하도록(쓸모 없으니까) 
생성자는 protected로 접근 제한해두었다.

반면 자식 클래스들은 직접 외부에서 객체로 생성할 것이기 때문에 생성자를 public으로 해둔다.



// 몬스터 생성
    // Creature == Player + Moster
    // Player(Knight, Archer, Mage)
    // Player(Slime, Orc, Skeleton)
    
    // Creature.cs
    // Player와 Monster의 부모 클래스. 플레이어와 몬스터가 가지는 공통적인 속성과 기능들을 모아두었다.

    public enum CreatureType
    {
        None,
        Player = 1,
        Monster = 2
    }

    class Creature
    {
        private CreatureType type; //private으로 선언
        protected int hp = 0;
        protected int attack = 0;

        protected Creature(CreatureType type)
        {
            this.type = type;
        }

        public void SetInfo(int hp, int attack)
        {
            this.hp = hp;
            this.attack = attack;
        }

        public int GetHP()
        {
            return hp;
        }

        public int GetAttack()
        {
            return attack;
        }

        public bool isDead()
        {
            return hp <= 0;
        }

        public void OnDamaged(int damage)
        {
            hp -= damage;
            if (hp < 0)
                hp = 0;
        }
    }
    
    
    
    // Player.cs
    public enum PlayerType
    {
        None = 0,
        Knight = 1,
        Archer = 2,
        Mage = 3
    }

    class Player : Creature
    {
        protected PlayerType type = PlayerType.None;

        protected Player(PlayerType type) : base(CreatureType.Player)
        {
            this.type = type;
        }

        public PlayerType GetPlayerType()
        {
            return type;
        }
    }

    class Knight : Player
    {
        public Kngiht() : base(PlayerType.Knight)
        {
            SetInfo(100, 10);
        }
    }

    class Archer : Player
    {
        public Archer() : base(PlayerType.Archer)
        {
            SetInfo(75, 12);
        }
    }

    class Mage : Player
    {
        public Mage() : base(PlayerType.Mage)
        {
            SetInfo(50, 15);
        }
    }
    
    
    
    
    // Monster.cs
    public enum MonsterType
    {
        None = 0,
        Slime = 1,
        Orc = 2,
        Skeleton = 3
    }

    class Monster : Creature
    {
        protected MonsterType type = MonsterType.None;

        protected Monster(MonsterType type) : base(CreatureType.Monster)
        {
            this.type = type;
        }

        public MonsterType GetMonsterType()
        {
            return type;
        }

        class Slime : Monster
        {
            public Slime() : base(MonsterType.Slime)
            {
                SetInfo(10, 1);
            }
        }

        class Orc : Monster
        {
            public Orc() : base(MonsterType.Orc)
            {
                SetInfo(20, 2);
            }
        }

        class Skeleton : Monster
        {
            public Skeleton() : base(MonsterType.Skeleton)
            {
                SetInfo(15, 5);
            }
        }
    }
    
    
    
    
    // 게임 진행
    // Game.cs -> 게임 로직
    // Program.cs -> 메인 함수. 무한 루프로 게임 로직 실행.

    public enum GameMode
    {
        None,
        Lobby,
        Town,
        Field
    }

    class Game
    {
        private GameMode mode = GameMode.Lobby;
        private Player player = null;
        private Monster monster = null;
        private Random rand = new Random();

        public void Process()
        {
            switch (mode)
            {
                case GameMode.Lobby:
                    ProcessLobby();
                    break;
                case GameMode.Town:
                    ProcessTown();
                    break;
                case GameMode.Field:
                    ProcessTown();
                    break;
            }
        }

        private void ProcessLobby()
        {
            Console.WriteLine("직업을 선택하세요");
            Console.WriteLine("[1] 기사");
            Console.WriteLine("[2] 궁수");
            Console.WriteLine("[3] 법사");

            string input = Console.ReadLine();
            
            switch input = Console.ReadLine();

            switch (input)
            {
                case "1":
                    player = new Knight();
                    mode = GameMode.Town
                    break;
                case "2":
                    player = new Archer();
                    mode = GameMode.Town
                    break;
                case "3":
                    player = new Mage();
                    mode = GameMode.Town
                    break;
            }
        }

        private void ProcessTown()
        {
            Console.WriteLine("마을에 입장하였습니다.");
            Console.WriteLine("[1] 필드로 간다.");
            Console.WriteLine("[2] 로비로 돌아가기.");

            string input = Console.ReadLine();

            switch (input)
            {
                case "1":
                    mode = GameMode.Field;
                    break;
                case "2":
                    mode = GameMode.Lobby;
                    break;
            }
        }

        private void ProcessField()
        {
            Console.WriteLine("필드에 입장했습니다.");
            Console.WriteLine("[1] 전투모드 돌입");
            Console.WriteLine("[2] 일정 확률로 마을로 도망");

            CreateRandomMonster();

            string input = Console.ReadLine();

            switch (input)
            {
                case "1":
                    ProcessFight();
                    break;
                case "2":
                    TryEscape();
                    break;
            }
        }

        private void CreateRandomMonster()
        {
            int randValue = rand.Next(0, 3);

            switch (randValue)
            {
                case 0:
                    monster = new Slime();
                    Console.WriteLine("슬라임이 스폰되었습니다.");
                    break;
                case 1:
                    monster = new Orc();
                    Console.WriteLine("오크가 스폰되었습니다.");
                    break;
                case 2:
                    monster = new Skeleton();
                    Console.WriteLine("스켈레톤이 스폰되었습니다.");
                    break;
            }
        }

        private void ProcessFight()
        {
            while (true)
            {
                int damage = player.GetAttack();
                monster.OnDamaged(damage);
                if (monster.IsDead())
                {
                    Console.WriteLine("승리했습니다!");
                    Console.WriteLine($"남은 체력 : {player.GetHP()}");
                    break;
                }

                damage = monster.GetAttack();
                player.OnDamaged(damage);
                if (player.IsDead())
                {
                    Console.WriteLine("패배했습니다.");
                    mode = GameMode.Lobby;
                    break;
                }
            }
        }

        private void TryEscape()
        {
            int randValue = rand.Next(0, 101);
            if (randValue <= 33)
                mode = GameMode.Town;
            else
                ProcessFight();
        }
        
    }


    
    // Program.cs
    class Program
    {
        static void Main(string[] args)
        {
            Game game = new Game();

            while (true)
            {
                game.Process();
            }
        }
    }
    
    
    
    
