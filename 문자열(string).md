// 부분 문자열 찾기
    // Contains

    string name = "Harry Potter";
    
    if(name.Contains("Harry"))
        Console.WriteLine("True");
    // True 출력
    
    
    // IndexOf
    string name = "Harry Potter";
    
    Console.WriteLine(name.IndexOf('P'));   // 6    6번째 자리에 있으니 6 출력
    Console.WriteLine(name.IndexOf('Z'));   // -1 존재하지 않으면 -1 출력


    // 변형
    // 덧붙이기: + 연산자
    string name = "Harry Potter";
    name = name + "Junior";

    Console.WriteLine(name);
    // Harry Potter Junior 출력
    
    
    // 소문자, 대문자로 변형 : ToLower, ToUpper
    string name = "Harry Potter";
    
    Console.WriteLine(name.ToLower());
    Console.WriteLine(name.ToUpper());
    // harry potter
    // HARRY POTTER
    
    
    // 특정 문자 바꾸기
    string name = "Harry Potter";
    string newName = name.Replace('r', 'l');
    Console.WriteLine(newName);
    // Hally Pottel
    
    
    // 분할
    // Split
    string name = "Harry Potter";
    string[] names = name.Split(new char[] { ' ' }); //' ' 공백을 기준으로 분할한 문자열들을 string [] 배열로 리턴.
    
    for(int i = 0; i < names.Length; i++)
        Console.WriteLine(names[i]);
    // Harry
    // Potter 출력
    // ' ' 공백기준으로 잘라서 "Harry", "Potter"로 만들고 이걸 string[] 배열에 집어 넣음. 배열의 0번째, 1번째 자리에 순서대로 들어감
    // 이를 0부터 names.Length 전까지 돌리며 Console.WriteLine(names[i]);로 출력해서 Harry와 Potter가 순서대로 출력된 것.
    
    
    //Split(char 배열)
    string text = "one\ttwo three:four,five six seven";
    string[] words = text.Split(new char[] { ' ', '\t', ':', '.', ',' });
    
    for (int i = 0; i < words.Length; i++)
        Console.WriteLine(words[i]);
    
    
    //
    string text = "Harry Potter";
    string[] words = text.Split("rry")
    
    for(int i = 0; i < words.Length; i++)
        Console.WriteLine(words[i]);
    
    
    //split(string 배열, StringSplitOptions)  인수로 넘긴 string 문자열 배열의 원소들을 기준으로 구분하고 구분하여 string[] 배열로 리턴한다.
    // 단 string 배열을 인수로 넘길 때는 두번째 인수가 반드시 필요함. 두번째 인수 포함하지 않으면 컴파일 에러 발생
    // 두번째 인수
    // StringSplitOptions.None 리턴 값에 빈 문자열이 포함됨
    // StringSplitOptions.RemoveEmptyEntries 리턴 값에 빈 문자열이 포함되지 않음.

    string text = "one<<two......three<four";
    string[] words = text.Split(new string[] { "<<", "......" }, System.StringSplitOptions.RemoveEmptyEntries);

    for (int i = 0; i < words.Length; i++)
        Console.WriteLine(words[i]);
    
    
    
    //Substring
    string name = "Harry Potter";
    Console.WriteLine(name.Substring(5));
    // Potter 출력   뒤에서 부터 5개
    
    
    // Substring(int)  호출한 문자열의 인수에 해당하는 인덱스부터 문자열 끝가지를 리턴함.
    string name = "Harry Potter";
    Console.WriteLine(name.Substring(5,4));
    // Pott 출력
    
    // 만약 Console.WriteLine(name.Substring(5));  이면 Potter가 출력 됨.
    
    
    //문자열 포맷  string.Format
    // C#에서는 항상 문자열을 간단한 인수의 순서에 따라 {0},{1},{2} 이런식으로 지정해주면 됨.
    int a = 10;
    int b = 5;
    string str = string.Format("{0} + {1} = {2}", a, b, a + b);
    Console.WriteLine(str);  // 10 + 5 = 15 출력됨
    
    
    // 기타
    //IsNullOfEmpty
    // string의 static 함수로, 인수로 넘긴 문자열이 null이거나 비어있으면 true 리턴
    string name = null;
    string.IsNullOrEmpty(name); // true 리턴
