// Generic
    // 클래스 정의시 여러가지 자료형에 대해 일반화.

    class MyList
    {
        private int[] arr = new int[10];

        public int GetItem(int i)
        {
            return arr[i];
        }
    }

    class MyfloatList
    {
        private float[] arr = new float[10];

        public float GetItem(int i)
        {
            return arr[i];
        }
    }

    class MyMonsterList
    {
        private Monster[] arr = new Monster[10];

        public Monster GetItem(int i)
        {
            return arr[i];
        }
    }
    
    // 같은 내용의 클래스라도 여러가지 자료형의 경우로 나누어야 한다면 위와 같이 일일이 나열해야 한다. 일반화시킬 필요가 있다. 굳이 여러개 쓰면 불편하잖어.
    
    
    // Object와 박싱/언박싱
    // Obejct -> int, float 같은 모든 자료형 및 모든 클래스의 조상. (사용자 지정 클래스의 조상도 Object이다.)
    
    // 박싱
    object obj = 3;
    object obj2 = "Hello World";
    // object 타입은 기본 자료형들을 비롯한 모든 클래스들의 조상이기 때문에 업 캐스팅 개념으로 int, string 같은 기본 자료형들을 object 하나로 참조할 수 있다. 이 과정을 박싱 이라고 한다.

    // 언박싱
    int num = (int)obj;
    string str = (string)obj2;
    // 다시 원래 자료형으로 되돌릴 땐 다운 캐스팅 개념으로 형변환 해주면 된다. 이 과정을 언박싱 이라고 한다.

    class MyList
    {
        private object[] arr = new object[10];
    }
    // 그러면 자료형들을 일반화시킬 때 위와 같이 object를 사용하면 되지 않을까?
    // 그래도 되긴 하지만, 박싱/언박싱 과정은 성능상 느리다. 따라서 비효율적이다.
    // object는 언제나 데이터를 참조하는 방식으로 저장하기 때문이다. 즉 진짜 데이터는 힙 메모리에 저장되고 변수 obj엔 그 주소가 저장된다.


    int n = 3;
    object obj = 3; // 박싱
    int num = (int)obj; // 언박싱
    
    // int인 n의 데이터 3은 스택 메모리의 n영역에 직접 저장된다.
    // object인 obj가 참조하는 데이터인 3은 힙 메모리에 저장되며, 스택 메모리의 obj영역엔 이 힙 메모리의 주소가 저장된다.
    // 박싱 -> 힙 메모리를 할당받는 과정이 필요하므로 성능면에서 깎임.
    // 힙 메모리에 있는 obj가 참조중인 데이터 3을 복사해 가져와 스택 메모리의 num영역에 직접 저장한다.
    // 언박싱 -> 힙 메모리에 있는 데이터를 빼내어 스택 영역으로 옮기는 과정이 필요하므로 이 역시 성능면에서 깎임.
    // 결론 : object는 박싱 언박싱 과정 때문에 성능이 좋지 않으므로 Generic을 통해 일반화를 한다. Generic은 컴파일 타임에 결정되기 때문에 더 빠르다.
    

    // Generic 일반화
    // Generic 클래스

    class MyList<T>
    {
        private T[] arr = new T[10];

        public T GetItem(int i)
        {
            return arr[i];
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            MyList<int> myIntList = new MyList<int>();
            MyList<Monster> myMonsterList = new MyList<Monster>();
        }
    }
    
    
    // 인자추가
    class MyList<T, M>
    {
        public T GetItem(M m)
        {
            return T[m];
        }
    }

    Dictionary<int, Monster> dic = new Dictionary<int, Monster>();
    
    // 일반화 할 특정 인자가 더 필요하다면 <class MyList <T, M> 이런식으로 T말고 추가 문자를 더 써주면 된다.
    // Dictionary 자료구조도 이렇게 Generic 인자를 2 개 사용하는 경우다.


    // where
    // C#에만 있는 문법으로 특수화를 할 때 사용한다. 구체화할 때 where T : type 👉 T를 type타입으로만 구체화하도록 제약을 둔다.
    class MyList<T> where T : Monster
    {
        
    }
    
    
    // Generic 일반 함수
    class Program
    {
        static void Test<T>(T input)
        {
            Console.WriteLine(input);
        }

        static void Main(string[] args)
        {
            Test<int>(3);
            Test<float>(3);
        }
    }
    
    // 이렇게 함수도 일반화할 수 있다. 함수 이름 오른쪽에 <T>만 붙여주고 일반화 할 자료형 자리를 T로 대체해주면 된다. 함수를 호출할 때도 함수 이름 오른쪽에 <T>만 붙여주면 된다. where로 제한도 할 수 있다.

