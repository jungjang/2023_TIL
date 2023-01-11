# 리액트 쿼리 사용법

After CRA

1. 리액트쿼리 라이브러리 설치 명령어 : yarn add react-query
2. query client 생성 : 쿼리와 서버의 데이터 캐시를 관리하는 클라이언트
3. QueryProvider : 자녀컴포넌트에게 캐시와 클라이언트 구성을 제공할 역할

useQuery : 서버에서 데이터를 가져오는데 쓰이는 훅

useQuery가 가지는 인수
1. 쿼리 키 : 쿼리의 이름
2. 쿼리함수 : 이 쿼리에 대한 데이터를 가져오는 함수(비동기함수여야 함)
3. 옵션 : 여러가지가 있는데 {staleTime: 2000} 같은 예로 넣을 수 있음

```
async function fetchPosts() {
  const response = await fetch(
    "https://jsonplaceholder.typicode.com/posts?_limit=10&_page=0"
  );
  return response.json();
}

  const { data, isLoading, isError, error } = useQuery("posts", fetchPosts);
```

리액트 쿼리는 요청이 실패할  경우 세 번 까지는 재시도를 해보고 <br/>
그 이후에 해당 데이터를 가져올 수 없다고 결정한다

### 리액트쿼리 개발자도구
- 앱에 추가할 수 있는 컴포넌트로 개발중인 모든 쿼리의 상태를 표시해준다.
- 쿼리키로 쿼리를 표시해주고 활성(active), 비활성(inactive), 만료(stale) 등 모든 쿼리 상태를 알려준다.
- 마지막으로 업데이트 된 타임스탬프를 보여준다.
- 쿼리에 의해 반환 된 데이터를 확인할 수 있는 데이터 탐색기 기능
- 쿼리를 볼 수 있는 쿼리 탐색기 기능
- 공식문서 : https://react-query.tanstack.com/devtools

### staleTime
- 데이터가 만료됐다고 판단하기 전까지 허용하는 시간 <br/>
  (ex. 웹사이트에 표시된 데이터가 10초까지는 그대로여도 괜찮다면 staleTime을 10초로 설정) 
- staleTime 디폴트값이 0인 이유 : 계속 업데이트되는게 실수로 업데이트 안된 데이터 보여주는거보다 나음(개발자피셜)

### cacheTime
- 나중에 다시 필요할 수 있는 데이터용
- 디폴트값 : 5분
- 캐시가 만료되면 클라이언트는 데이터를 다시 사용할 수 없음

### Data Prefetching 
- 데이터를 미리 가져와 캐시에 넣어서 사용자가 기다릴 필요가 없도록 하는 것
- 사용자가 사용할 법한 모든 데이터에 프리페칭을 사용함
- const queryClient = useQueryClient(); 로 정의 하고 시작
- onClick이벤트로 하는 것보다 useEffect로 활용하는게 좋다

### isFetching VS isLoading
- isFetching : async 쿼리 함수가 해결되지 않았을 때 참에 해당 (아직 데이터를 가져오는 중)
- isLoading : isFetching이 참이면서 쿼리에 대해 캐시된 데이터가 없는 상태(isFetching의 부분집합이라고 생각)
- 즉, isLoading이 참이다 => isFetching 또한 항상 참임

### Mutations
- 서버에 데이터를 업데이트하도록 서버에 네트워크 호출을 실시
- 추가, 삭제, 변경같은 작업
- useQuery와 상당히 유사함
- mutate함수를 반환함 ( 이는 우리가 변경사항을 토대로 서버를 호출할 때 사용함 )
- 데이터를 저장하지 않으므로 쿼리키가 필요 없음
- 우리가 인수로 전달하는 muatation함수는 그 자체도 인수를 받을 수 있다.
- isLoading은 존재하지만 isFetching은 존재하지 않음( 캐시된 항목이 없어서 )
- useQuery가 요청이실패할경우 자동으로 재요청을 세 번까지 하지만 , useMutation은 재요청을 하지 않는다 (임의로 설정은 가능)
- 공식문서 : https://react-query.tanstack.com/guides/mutations
- 
- 
