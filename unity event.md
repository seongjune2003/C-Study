// 유니티 이벤트
    
    // 유니티 이벤트란? Unity Event
    // C # 의 delegate와 event 기능을 사용하기 쉽게 유니티에서 제공하는 것
    
    // 이벤트란? 
    // 어떤 이벤트가 발생하면 그 이벤트에 등록해 둔 모든 함수들이 자동으로 발동된다.
    // 이벤트를 발생시키는 측도, 이벤트에 등록되있는 함수들도 서로에게 관심이 없다.
    //      등록되있는 함수들은 언제 발동될지, 어떻게 발동될지 관심이 없다.
    //      이벤트를 발생시키는 측도 자신에게 어떤 함수들이 등록되어있는지 관심이 없다.
    // 코드들이 스파게티처럼 엮이지 않아 코드가 간결해진다.
    
    
    
    // 유니티 이벤트 사용한 경우
    // using UnityEngine.Events를 해주어야 한다.
    
    // 유니티 이벤트 원리
    // 실행 시키는 이벤트 측, 실행 되는 측. 둘 다 서로를 모른다. 그저 이벤트에 등록해놔서 발동되는 것일 뿐.     // 이게 델리게이트 사용하는 목적이기도 함.
    // 다른 사람하고 같이 개발할 때 서로 각자 짠 코드를 알 필요없이 해당 함수가 있어야 하는 스크립트 파일에 추가만 해두면 되는거지.
    // 실행시키는 측, 실행 되는 측 둘다 서로를 몰라도 이벤트에 등록만 되어 있다면 알아서 실행된다.
    // 따라서 스파게티처럼 연결될 필요가 없어 코드가 훨씬 깔끔해진다.
    
    // 플레이어가 죽는 이벤트인 PlayerHealth.cs 의 Dead() 이벤트에
    // 플레이어가 죽으면 동시에 발동시킬 UIManager.cs, AchivementSystem.cs, GameManger.cs의 각 함수를 등록한다.
    
    // PlayerHealth.cs 과 UIManager, AchivementSystem, GameManger 는 서로에 대해 몰라도 된다. 서로에 대해 참조하고 있을 필요가 전혀 없다.
    // 플레이어가 죽은 후 발동시킬 함수를 가진 오브젝트(스크립트)들을 유니티 슬롯에 일일이 넣어줄 필요도 없고
    // 플레이어가 죽은 후 발동시킬 스크립트가 추가되더라도 또 참조 변수를 새로 선언해줄 필요가 없다.
    //      그저 이벤트에 추가 등록해주면 될 뿐이다.
    
    // 이걸 사용하면 어떻게 되냐면
    
    // PlayerHealth.cs  유니티 이벤트 안했을때
    public class PlayerHealth : MonoBehaviour
    {
        public UIManager uiManager;                     // 여기에 일일히 붙여줘야 하고
        public AchivementSystem achivementSystem;
        public GameManager gamaManager;

        private void Dead()
        {
            uiManager.OnPlayerDead();                   // 그 붙여진 함수 내부에 뭐가 있는지 다 알아야해서 귀찮음
            achivementSystem.UnLockAchivement("뉴턴의 법칙");
            gamaManager.OnPlayerDead();

            Debug.Log("죽었다!");
            Destroy(gameObject);
        }

        void OnTriggerEnter(Collider other)
        {
            Dead();
        }

    }
    
    
    
    // PlayerHealth.cs   유니티 이벤트 사용했을 때
    using UnityEngine.Events;       // 유니티 이벤트 사용하게 이 네임스페이스 추가해주고
    
    public class PlayerHealth : MonoBehaviour
    {
        public UnityEvent onPlayerDead;     // 그냥 유니티 이벤트 하나 새로 선언해서 거기다 실행할 거 다 넣고

        private void Dead()
        {
            onPlayerDead.Invoke();         // 여기서 불러와 버리면 끝이지.  코드 훨씬 간단해졌지?

            Debug.Log("죽었다!");
            Destroy(gameObject);
        }

        void OnTriggerEnter(Collider other)
        {
            Dead();
        }

    }
    
    //  using UnityEngine.Events;       유니티 이벤트를 사용하기 위해선 필수
    //  public UnityEvent onPlayerDead      onPlayerDead라는 이벤트를 선언했다.
    //  onPlayerDead.Invoke();   Dead() 함수 내부에서 onPlayerDead 이벤트를 발동시킨다   onPlayerDead 이벤트에 등록된 타 스크립트의 모든 함수들이 발동된다.
    //  코드가 훨씬 간결해졌다!       실행할 함수를 가진 타 스크립트들을 참조하고 일일이 함수를 실행해 줄 필요가 없어졌으므로.
    
    
    
    // 유니티 이벤트 등록하기
    // 이벤트가 발동 할 시 실행될 함수 명단 등록     인스펙터 창에서 등록
    
    // 1. 플레이어가 죽는 이벤트가 발생할시 실행시킬 함수가 속해 있는 스크립트가 붙은 오브젝트들을 드래그 앤 드롭 해준다
    // GameManager - GameManger
    // Canvas - UIManager, AchivementSystem
    // 2. 실행할 함수를 드롭 다운에서 선택해준다.
    // 3. “뉴턴의 법칙”에서 볼 수 있듯 매개변수가 있는, 입력이 필요한 함수들은 여기에 인수로 넘길 입력 내용도 같이 적어줄 수 있다.
    
