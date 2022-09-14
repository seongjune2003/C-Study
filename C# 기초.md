// 배열
    for (int i = 0, i < 10, i = i+2){
        Debug.Log("현재순번" + i);
    }
    Debug.Log("루프 끝");


    int[] scores = new int[10];
    scores = new int[20];

    void Start()
    {
        int[] scores = new int[10];

        scores[0] = 90;
        scores[1] = 45;
        scores[2] = 60;
        scores[3] = 70;
        scores[4] = 56;
        scores[5] = 80;
        scores[6] = 90;
        scores[7] = 100;
        scores[8] = 45;
        scores[9] = 14;

        
        // score[10] = 30; 이건 out of index
        
        for (int i=0, i<10, i++)
        {
            Debug.Log("학생" + i + "번째의 점수" + scores[i]);
        }

        scores = new int[20];       // 이렇게 하면 기존 원소들 싹 날라가고 새로운 20개 크기의 빈 배열 할당됨.


    }


    public class Animal
    {
        public string name;     // public을 꼭 붙어주어야 외부에서도 보고 사용할 수 있다. (디폴트 private)
        public string sound;
        public float weight;
    }

    public class HelloClass : MonoBehavior
    {
        void Start()
        {
            // 각각의 동물 객체마다 name, sound, weight 속성을 가지고 있지만 값은 전부 다 다름.
            // 객체들은 서로 구분되고 독립적인 존재들

            Animal jack = new Animal();   // Animal 객체 "jack"을 찍어내어 탄생시킴
            jack.name = "Jack";     // // name이 public이 아니였다면 에러
            jack.sound = "Bark";
            jack.weight = 4.5f;

            Animal annie = new Animal();
            annie.name = "ANNIE";
            annie.sound = "Wee";
            annie.weight = 0.8f;

            Animal nate = new Animal();
            nate.name = "NATE";
            nate.sound = "NYaa";
            nate.weight = 1.2f;

            nate = jack;            // jack이 가지고 있는 정보를 nate에 덮어 씌운다.   이 경우 기존에 nate가 참조하고 있던 NATE는 가비지가 된다. (접근할 방법이 없다)
            nate.name = "JIMMY"     // jack의 이름까지도 바뀐다!   // 변수는 3개 인데 오브젝트는 2개인 상황으로 변한 것.


            Debug.Log(jack.name);
            Debug.Log(nate.name);
        }
    }
    
    // 변수는 값을 가리키는 이름표임을 기억하자.
    
    
    // Call by Reference
    // 기존에 미리 만들어져 존재하는 것을 가져와서 쓴다는 개념.

    public class jump : MonoBehavior
    {
        public Rigidbody rb;

        void Start()
        {
            rb.AddForce(0, 1000, 0);
        }

        void Update()
        {
            
        }
    }
    
    // public Rigidbody rb;
    // 변수는 오브젝트 그 자체가 아니라 오브젝트를 가리키는 이름표라는 것을 기억하자.
    // public으로 해놓으면 유니티 인터페이스에서 Rigidbody 컴포넌트 객체를 드래그 앤 드롭할 수 있는 슬롯이 열린다.
    // 이 슬롯에 오브젝트에 실제로 현재 붙어있는 Rigidbody 컴포넌트를 드래그 앤 드롭하면 이제 rb라는 이름표가 가리키는 이 컴포넌트에 접근할 수 있게 된다.
    
    // rb.AddForce(0, 1000, 0);
    // 이제 rb 변수(이름표)로 실존하는 이 컴포넌트를 접근할 수 있다.
    // rb라는 이름으로 슬롯에 드래그 앤 드롭한 실존하는 이 컴포넌트에 접근하여 AddForce 기능을 하게끔 함.
    
