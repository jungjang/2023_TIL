# 무한스크롤

### 무한스크롤 입문
- 사용자가 스크롤 할 때마다 새로운 데이터를 가져오는 것
- 모든 데이터를 한 번에 가져오는 것보다 효율적
- 엄청난 양의 데이터가 구축되어있는 경우 효율성이 더 커짐
- 사용자가 버튼을 클릭해서 새로운 데이터를 요청하거나 <br/>
  페이지의 특정 지점을 스크롤 했을 때 새 데이터를 가져오게 하는 것 (이 파일,강의는 이 후자를 다룸)
  (사용자가 데이터의 하단으로 오면 새로운 데이터를 가져와서 중단 없이 계속 스크롤 할 수 있도록)
- useInfiniteQuery 훅 사용
- useInfiniteQuery는 다음 쿼리가 뭘지 추적한다. (이 경우 다음 쿼리가 데이터의 일부로서 반환됨)

### useInfiniteQuery 와 useQuery의 차이점
- 반환 객체에서 반환된 데이터 프로퍼티의 형태가 다름<br/>
  useQuery에서는 데이터는 단순히 쿼리 함수에서 반환되는 데이터임<br/>
  useInfiniteQuery에서 데이터는 두 개의 프로퍼티가 있음<br/>
  (pages : 하나는 데이터 페이지 객체의 배열인 '페이지', pageParams : 각 페이지의 매개변수(많이 사용되지는 않음))<br/>
  모든 쿼리는 페이지 배열에 고유한 요소를 가지고 있고 그 요소는 해당 쿼리에 대한 데이터에 <br/>
  페이지 진행되면서 쿼리도 바뀜
  pageParams는 검색된 쿼리의 키를 추적함
  
### infiniteQuery의 구문, 원리
- useInfiniteQuery에 옵션을 사용하는 방식
- getNextPageParam 옵션으로 다음 페이지로 가는 방식을 정의한다. (lastPage or allPages)<br/>
  (lastPage 는 다음 페이지의 url이 무엇인지 알려줌)
- useQuery와는 다른 '반환객체의 몇가지 프로퍼티'가 있는데 무한스크롤을 위해 이를 사용<br/>
  (fetchNextPage : 사용자가 더 많은 데이터를 요청할 때 쓰는 함수(버튼 혹은 일정 지점까지 스크롤 했을 때)<br/>
   hasNextPage : getNextPageParam 함수의 반환 값을 기반으로 하는데 이 프로퍼티를 useInfiniteQuery에 전달해서 마지막 쿼리의 데이터를 어떻게 사용할지 지시<br/>
                (hasNextPage가 undefined면 더 이상 데이터가 없는거고, 이 경우 false가 됨)<br/>
   isFetchingNextPage : 다음페이지를 가져오는지 아니면 일반적인 페칭인지 구별하게 해줌 <br/>                    
