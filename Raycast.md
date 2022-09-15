// 레이캐스트란?
    // 레이캐스트 : 오브젝트의 정중앙에서 눈에 보이지 않는 광선을 날려서 특정 거리 이내에 오브젝트가 있는지 없는지를 충돌 감지해주는 과정.
    
    
    // RayInteracion.h
    // 1인칭으로 플레이어가 눈 앞에 응시하고 있는 오브젝트를 다른 곳으로 옮기는 코드를 작성해 보자.
    // 1. 카메라 오브젝트의 정중앙에서 광선을 쏜다.
    // 2. 마우스 좌클릭 하는 동안 레이캐스트를 통해 광선에 충돌 감지 되는 Collider가 있는지 검사해야한다.
    // 3. 마우스 좌클릭 하는 동안 광선에 감지 된 오브젝트를 카메라의 시야를 따라가게끔 이동시킨다.
    
    // Hierarchy
    //      바닥이 될 Plane 오브젝트
    //      1인칭 카메라 FPSController 오브젝트
    //          FPS 1인칭 카메라가 될 프리팹 FPSController을 오브젝화시킨 후 여기에 RayInteracion.h을 붙인다.
    //          이 프리팹 안에 자식 오브젝트로 카메라가 붙어있는 상태.
    
    // Cube오브젝트
    //      FPSController가 레이캐스트로 감지할 대상.
    //      대충 카메라 앞에 위치시켜주자.
    
    
    // Camera.ViewportToWorldPoint, Physics.RaycastPermalink
    public class RayInteration : MonoBehaviour
    {
        private Camera playerCam;

        public float distance = 100f;

        void Start()
        {
            playerCam = Camera.main;
        }

        void Update()
        {
            Vector3 rayOrigin = playerCam.ViewportToWorldPoint(new Vector3(0.5f, 0.5f, 0.0f));

            Vector3 rayDir = playerCam.transform.forward;

            if (Input.GetMouseButtonDown(0))        // 마우스 왼클릭
            {
                if (Physics.Raycast(rayOrigin, rayDir, distance))
                {
                    Debug.Log("뭔가 광선에 걸렸다.");
                }
            }
        }
    }

    // private Camera playerCam;
    //  카메라 오브젝트
    //  광선을 쏘는 곳이 카메라니 카메라의 위치를 알아야하기 때문에 사용
    
    // public float distance = 100f;
    //   광선의 길이를 100으로 설정
    //      100짜리 광선에 닿으면 감지하게 할 것
    
    // void Start()
    // playerCam = Camera.main;
    //      "MainCamera" 태그가 붙은 현재 활성화 되어 있는 카메라.
    //      playerCam은 현재 활성화되어 있는 메인인 카메라로 초기화 됐다.
    
    // void Update()
    //     Vector3 rayOrigin = playerCam.ViewportToWorldPoint(new Vector3(0.5f, 0.5f, 0.0f));
    // 광선 발사 위치 - 카메라 뷰포트의 정중앙에서부터 광선이 발사되게 할 것이다.
    
    // Camera.ViewportToWorldPoint(Vector3)
    //    카메라 오브젝트에 내장되어 있는 함수로서 카메라가 찍고 있는 화면(뷰포트)상의 위치를 Vector3로 넘기면 그 위치를 실제 게임 월드의 위치로 리턴해준다.
    
    // new Vector3(0.5f, 0.5f, 0.0f)
    //      카메라가 찍고 있는 화면은 (x, y) 2D 좌표를 사용하며 화면의 좌측 하단은 (0,0)이며 화면의 우측 상단은 (1,1)이다.
    //      z 값은 카메라 오브젝트로부터 실제 카메라가 찍고 있는 화면까지의 실제 게임 월드 거리, 즉 카메라의 깊이를 의미한다.
    //      (0.5f, 0.5f, 0.0f)를 넘겨준다는 것은 카메라 화면의 정중앙 + 화면과 카메라 오브젝트는 위치를 일치하게 라는 듯이다.
    //    playerCam.transform.position을 사용해도 된다.
    //카메라가 정중앙으로 찍고 있는 화면상 위치의 실제 게임 월드 위치에서 광선을 발사할 것이다.
    
    // Vector3 rayDir = playerCam.transform.forward;
    // 발사 방향
    // 즉, 카메라의 앞쪽 방향 벡터

    // if (Input.GetMouseButtonDown(0))
    // 좌클릭을 누르는 순간 레이캐스트, 카메라 중심에서 눈에 보이지 않는 광선을 쏴서 광선에 닿는 Collider가 있는지 감지할 것이다.
    // if (Physics.Raycast(rayOrigin, rayDir, distance))
    
    //      광선을 쏘고 이에 감지되는 오브젝트가 있다면 True 리턴
    //      Physics.Raycast(rayOrigin, rayDir, distance)
    //      Raycast는 물리에 관련된 함수와 데이터를 모아둔 집합 Physics 에서 지원한다.
    //      매개변수로 (발사 위치, 발사 방향, 광선 거리)를 넘겨준다.
    
    // 여기까지 하고 실행하면 Cube와 Plane(바닥) 오브젝트를 카메라 화면 정중앙에 담게끔 바라보고 마우스 좌클릭 하면 “뭔가 광선에 걸렸다!” 콘솔 메세지를 출력한다.
    
    
    // Layer 설정. Debug.drawRay
    public class RayInteration : MonoBehaviour
    {
        private Camera playerCam;
        public float distance = 100f;
        public LayerMask whatIsTarget;

        void Start()
        {
            playerCam = Camera.main;
        }

        void Update()
        {
            Vector3 rayOrigin = playerCam.ViewportToWorldPoint(new Vector3(0.5f, 0.5f, 0.0f));

            Vector3 rayDir = playerCam.transform.forward;

            Debug.DrawRay(ray.origin, ray.direction * 100f, Color.green);

            if (Input.GetMouseButtonDown(0))
            {
                if (Physics.Raycast(rayOrigin, rayDir, distance, whatIsTarget))
                {
                    Debug.Log("뭔가 광선에 걸렸다.")
                }
            }
        }
    }
    
    //Plane(바닥)은 광선 감지 처리 안하고 싶고 Cube만 광선 감지를 하고 싶다. Cube에 Layer를 붙여 해당 Layer만 광선에 충돌 감지하도록 하자.
    // 광선이 씬창에 보이게하기 위해 Debug.drawRay 로 광선을 그려주었다.
    
    // public LayerMask whatIsTarget;
    //      어떤 레이어를 가진 Collider만 충돌 처리를 할 것인지 레이어 설정.
    // 우선 새로운 Layer를 추가해서 Cube에 붙여주면 (“Interactable”이라는 이름으로 했다.) 유니티에서 드롭 다운 슬롯이 열릴텐데
    // 여기서 Cube에 붙어있는 layer를 선택한다.
    // Cube만 광선의 충돌 감지에 걸릴 수 있도록.     (CompareTag랑 비슷한 것)
    
    // Debug.DrawRay(ray.origin, ray.direction * 100f, Color.green)
    // 개발자가 시각적으로 광선을 볼 수 있도록 광선을 그려주는 함수다.
    // Debug에서 지원함
    // 실제 게임에는 반영되지 않는다. 오직 개발자가 씬창에서 광선을 볼 수 있게 도와주는 역할!
    // 광선이 씬창에서 초록색 선으로 그려지게 된다.
    
    // 이제 Plane(바닥)을 바라보고 좌클 눌러도 충돌 감지 되지 않는다. Cube만 충돌 감지 함
    
    
    
    // RaycastHit, 광선에 감지된 오브젝트의 색깔을 바꾸게끔
    public class RayInteration : MonoBehaviour
    {
        private Camera playerCam;
        public float distance = 100f;

        public LayerMask whatIsTarget;

        void Start()
        {
            playerCam = Camera.main;
        }

        void Update()
        {
            Vector3 rayOrigin = playerCam.ViewportToWorldPoint(new Vector3(0.5f, 0.5f, 0.0f));

            Vector rayDir = playerCam.transform.forward;

            if (Input.GetMouseButtonDown(0))
            {
                RaycastHit hit;

                if (Physics.Raycast(rayOrigin, rayDir, out hit, distance, whatIsTarget))
                {
                    GameObject hitTarget = hit.collider.gameObject;
                    hitTarget.GetComponent<Renderer>().material.color = Color.Red;

                    Debug.Log(hit.collider.gameObject.name);
                }
            }
        }
    }

    // RaycastHit hit;
    //      레이캐스트로부터 정보를 얻기 위한 타입으로 광선에 감지된 Collider의 정보를 담는 컨테이너다
    //      변수 RaycastHit hit 일때
    //          hit.normal : 광선에 감지된 Collider의 노말 벡터 (충돌 표면의 방향벡터)
    //          hit.distance : 광선 발사 위치로부터 광선에 감지된 Collider까지의 거리
    //          hit.point : 광선에 감지된 Collider의 충돌 위치벡터
    //          hit.collider : 광선에 감지된 Collider

    // if (Physics.Raycast(rayOrigin, rayDir, out hit, distance, whatIsTarget))
    //      hit을 out으로 넘기면 입력으로 들어간 값이 내부에서 어떤 값을 지정받고 빠져나온다.
    //      raycast가 hit을 받게되면 이 hit에 정보들을 채워서 넘겨준다. 그런 다음에 hit로부터 정보를 가져온다.
    //      Physics.Raycast 함수의 실행이 끝나자마자 hit에 광선에 충돌 감지된 Collider의 정보가 들어가게 된다.
    
    // GameObject hitTarget = hit.collider.gameObject;
    // 광선에 충돌 감지된 Collider 컴포넌트를 가진 오브젝트를 hitTarget에 대입한다.
    
    // hitTarget.GetComponent<Renderer>().material.color = Color.red;
    // 광선에 충돌 감지된 Collider 오브젝트의 색깔을 빨간색으로 바꿈
    // GetComponent로 Renderer 컴포넌트 가져오고 material.color 접근함.
    
    // Debug.Log(hit.collider.gameObject.name);
    //  광선에 충돌 감지된 Collider 오브젝트의 이름 출력
    
    // 여기까지 하고 실행하면 좌클릭했을때 카메라 중앙에 오브젝트가 들어온다면 해당 오브젝트의 색깔이 빨간색으로 바뀐다.
    
    
    
    // Ray, 광선에 닿는 오브젝트 잡고 이동시키기
    public class RayInteration : MonoBehaviour
    {
        private Camera playerCam;
        public float distance = 100f;
        
        private Transform moveTarget

        private float targetDistance;

        private LayerMask whatIsTarget;

        void Start()
        {
            playerCam = Camera.main;
        }

        void Update()
        {
            Ray ray = new Ray(rayOrigin, rayDir);

            if (Input.GetMouseButtonDown(0))
            {
                RaycastHit hit;

                if (Physics.RayCast(ray, out hit, distance, whatIsTarget))
                {
                    GameObject hitTarget = hit.collider.gameObject;
                    hitTarget.GetComponent<Renderer>().material.color = Color.Red;

                    Debug.Log(hit.collider.gameObject.name);
                    Debug.Log("뭔가 광선에 걸렸다.");

                    moveTarget = hitTarget.transform;
                    targetDistance = hit.distance;
                }
            }

            if (Input.GetMouseButtonUp(0))      // 왼클릭 뗐을때
            {
                if (moveTarget != null)     // 광선에 부딪힌게 있어서 좌표값이 반환 되었다면
                {
                    moveTarget.GetComponent<Renderer>().material.color = Color.White;
                }

                moveTarget = null;
            }

            if (moveTarget != null)
            {
                moveTarget.position = ray.origin + ray.direction * targetDistance;
            }
        }
    }

    // private Transform moveTarget;
    // 광선에 충돌 감지된 오브젝트를 Transform 타입으로 여기에 넣을 것

    // private float targetDistance;
    // 광선에 충돌 감지된 오브젝트로부터 광선을 발사한 카메라 위치까지의 거리
    // 거리를 유지하면서 오브젝트를 이동시킬거라서 필요
    
    // Ray ray = new Ray(rayOrigin, rayDir);
    //      발사 위치와 발사 방향을 담는 광선

    // if (Physics.Raycast(ray, out hit, distance, whatIsTarget))
    //      발사위치와 발사 방향을 ray에 담아 넘긴다.
    
    // moveTarget = hitTarget.transform;
    // 광선에 충돌 감지된 오브젝트의 위치
    
    // targetDistance = hit.distance;
    // 광선에 충돌 감지된 오브젝트로부터 광선을 발사한 카메라 위치까지의 거리
    
    // if(Input.GetMouseButtonUp(0))
    //      마우스 좌클에서 손을 떼자마자
    //      if(moveTarget != null)
    //      광선에 충돌에 감지되서 moveTarget에 저장된게 있다면
    //          moveTarget.GetComponent<Renderer>().material.color = Color.white;
    //          원래 색인 하얀색으로 돌려준다.
    //          moveTarget = null (null로 초기화)

    // if(moveTarget != null)
    // 계속 마우스 좌클을 유지하고 있는 동안이 됨
    // moveTarget.position = ray.origin + ray.direction * targetDistance;
    //      거리를 유지한 채로 광선에 감지된 오브젝트의 위치를 광선의 위치에서 광선이 쏘는 방향으로 옮겨준다.
    //      거리를 유지한 채 카메라가 보는 방향으로 이동시키는게 된다.
    
    
    
    // 레이캐스트를 사용하는 경우
    // RayCast는 주로 정확한 물리처리를 요구할때 사용한다.
    //      OntriggerEnter OnCollision은 메세지 기반 프레임 기반 처리기 떄문에 딱 정확할때 처리 못할 수도 있다.
    //      Raycast로 아래에 광선을 쏴서 바닥을 검사하는 등등의 방식으로 더 많이 씀    (IsGrounded 구할 때 보통 쓰지)
    // FPS는 레이케스트를 많이 쓴다. 광선을 쏴서 거기에 닿으면 데미지를 깎는 식으로!

