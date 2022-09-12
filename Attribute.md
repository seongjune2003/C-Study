// Attribute
    class Program
    {
        class Important : System.Attribute
        {
            private string message;

            public Important(string message)
            {
                this.message = message;
            }
        }

        class Monster
        {
            [Important("Very Important")] public int hp;

            protected int attack;
            private float speed;

            void Attack()
            {
                
            }

            static void Main(string[] args)
            {
                Monster monster = new Monster();
                Type type = monster.GetType();
                FieldInfo[] fields = type.GetField();

                var attributes = fields[0].GetCustomAttributes();   // "very important"
            }
        }
    }
    
    // Attribute -> 특정 멤버나 클래스나 함수 등등에 추가적인 메타 데이터를 붙여 줌.
    // 어떤 Attributes 를 클래스나 멤버 혹은 함수 등등에 적용하려면 적용하려는 대상의 바로 윗줄에 [Attribute 이름]을 써주면 된다.
    
    //주석은 개발자가 참고하기 위해 사용하는 것이며 런타임 때는 전혀 고려되지 않는다. 
    // 이와 달리 Attribute는 컴퓨터가 런타임에 참고하기 위해 사용되는 주석과 같은 존재이며 컴퓨터가 런타임에 중에도 Attribute가 붙은 대상을 체크하여 그에 관한 작업을 한다.
    
    // 유니티에서 주로 사용하는 Attribute 로는 [SerializedField]가 있는데,
    // 이 Attribute를 위에 써 준 멤버 변수는 private이더라도 유니티에서 UI를 열어주는 멤버 변수라고 유니티에게 추가 정보를 주는 것과 같다. 
    // 특정 멤컴퓨터에게 하나 이상의 추가적인 메타 데이터(Attribute)를 알려주는식이다.
    
    // 사용자 지정 Attribute
    class Important : System.Attribute
    {
        private string message;

        public Important(string message)
        {
            this.message = message;
        }
    }
    // 사용자 지정 Attribute를 만드려면 System.Attribute을 상속받는 클래스를 만들면 된다. Important라는 Attribute를 만들었다.
    
    [Important("Very Important")]
    public int hp;
    // hp멤버 변수에 Important Attribute를 붙여주었다.
    // 즉 hp에 추가적인 데이터를 덧붙여 주었고 이를 컴퓨터가 런타임에 알 수 있다!
    // hp 멤버 변수는 “Very Important”라는 문자열이 담긴 message를 추가적으로 담고 있다.

    Monster monster = new Monster();
    Type type = monster.GetType();
    FieldInfo[] fields = type.GetFields();

    var attributes = fields[0].GetCustomAttributes();
    
