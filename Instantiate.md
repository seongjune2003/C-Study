 /*
    
    // 인스턴스화 : Instantiate     인스턴스는 프리팹이랑 같이 보면 됨. 없는 상황에서 만들때 쓰는 거.
    // 미리 만들어 둔 오브젝트를 실시간으로 게임 도중에 필요한 만큼 찍어내는 것
    // ex) 총알, 몬스터 같은 것들은 게임 플레이 도중에 생성 되야하는 오브젝트들이다
    
    // Spawner.cs
    // 오브젝트 원본을 넣어주면 그 원본을 게임 도중에 찍어내는 역할을 하는 스크립트
    public class Spawner : MonoBehaviour
    {
        public GameObject target;

        void Start()
        {
            Instantiate(target);
        }
    }
    
    
    //public GameObject target;
    // 게임 도중에 찍어낼 오브젝트를 참조할 변수
    // 찍어낼 오브젝트를 유니티에서 슬롯에 드래그 앤 드롭 해줄 것이다.
    
    // Instantiate(target);
    // target 변수가 참조하는 오브젝트를 게임 도중에 찍어내는 함수
    // 찍어낸 오브젝트를 리턴한다.  게임을 실행시키면 target이 참조하는 오브젝트를 1개 찍어낸다.
    
    // 1. Empty Object를 만든 후 이 Spawner.cs 스크립트를 붙여준다.(이름은 Spawner)
    
    
 
    
    //Instantiate(찍어낼 오브젝트, 찍어낼 위치, 찍을 때 회전값)

    public class Spawner : MonoBehaviour
    {
        public GameObject target;       // prefab으로 만든 Ball
        public Transfrom spawnPosition;     // 스폰 위치를 나타내는 빈 오브젝트의 Transform

        void Start()
        {
            Instantiate(target, spawnPosition.position,, spawnPosition.rotation);
        }
    }
    
    // 빈 오브젝트(이름은 SpawnPosition)를 하나 더 만들어 Spawner Object의 spawnPosition 슬롯에 넣어준다.
    //      이 빈 오브젝트(SpawnPosition)는 스폰 위치를 나타내는 역할로 사용할 것이다.
    
    
    // 찍어낸 오브젝트 리턴 받기
    // Instantiate 함수는 찍어낸 오브젝트를 리턴한다.
    
    // Spawner.cs
    public class Spawner : MonoBehaviour
    {
        public GameObject target;       // prefab으로 만든 Ball
        public Transfrom spawnPosition;     // 스폰 위치를 나타내는 빈 오브젝트의 Transform

        void Start()
        {
            GameObject instance = Instantiate(target, spawnPosition.position,, spawnPosition.rotation);

            Debug.Log(instance.name);
        }
    }
    // GameObject instance: 변수가 플레이 도중 새롭게 생성된 Ball Object 인스턴스를 참조하게 될 것이다. Instantiate 함수가 리턴해주어서 가능한 일.
    // Debug.Log(instance.name); : 게임 실행 후 Ball 인스턴스가 생성되면 콘솔에 “Ball(clone)” 메세지가 출력된다.


    public class Spawner : MonoBehaviour
    {
        public Rigidbody target;    // ball Prefab은 Rigidbody 컴포넌트를 가지고 있는 상태.

        public Transform spawnPosition;

        void Start()
        {
            Rigidbody instance = Instantiate(target, spawnPosition.position, spawnPosition.rotation);

            instance.AddForce(0, 1000, 0);
        }
    }
    
    // public Rigidbody target
    //     본인에게 붙어있는 Rigidbody 갖고 오려면 RIgidbody 컴포넌트를 슬롯에 드래그 앤 드롭하면 되지만
    //      나 말고 다른 오브젝트에게 붙어 있는 Rigidbody를 가져오려면 그냥 슬롯에 그 Rigidbody를 가지고 있는 오브젝트를 드래그 앤 드롭하면 된다.
    //      Rigidbody가 없는 오브젝트는 드래그 앤 드롭이 불가능하다.
    
    // Rigidbody instance = Instantiate(target)
    //      target은 Rigidbody이기 때문에 Instantiate 또한 Rigidbody 타입으로 인스턴스를 리턴한다.
    //      instance.AddForce(0, 1000, 0); 이렇게 사용 가능. Instantiate가 Rigidbody 타입으로 리턴해줘서 instance는 Rigidbody 타입이므로.


    public class Spawner : MonoBehaviour
    {
        public GameObject target;

        public Transform spawnPosition;

        void Start()
        {
            GameObject instance = Instantiate(target, spawnPosition.position, spawnPosition.rotation);

            instance.GetComponent<Rigidbody>().AddForce(0, 1000, 0);       // GetComponent로 Rigidbody를 가져와.
        }
    }

    // 위 코드와 같이 사용할 수도 있다! GameObject로 리턴 받았는데 Rigidbody 컴포넌트를 쓰고 싶다면 GetComPonent로 Rigidbody 타입을 가져오면 됨


*/
