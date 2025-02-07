# 원티드 프리온보딩 안드로이드
# 1팀 MovieReviewApp

## 팀원

<div align="center">
  <table style="font-weight : bold">
      <tr>
          <td align="center">
              <a href="https://github.com/tjrkdgnl">                 
                  <img alt="tjrkdgnl" src="https://avatars.githubusercontent.com/tjrkdgnl" width="80" />            
              </a>
          </td>
          <td align="center">
              <a href="https://github.com/gyurim">                 
                  <img alt="gyurim" src="https://avatars.githubusercontent.com/gyurim" width="80" />            
              </a>
          </td>
          <td align="center">
              <a href="https://github.com/014967 ">                 
                  <img alt="lsy524" src="https://avatars.githubusercontent.com/014967 " width="80" />            
              </a>
          </td>
          <td align="center">
              <a href="https://github.com/gksgpd97 ">                 
                  <img alt="hoyahozz" src="https://avatars.githubusercontent.com/gksgpd97 " width="80" />            
              </a>
          </td>
          <td align="center">
              <a href="https://github.com/INAH-PAK ">                 
                  <img alt="hoyahozz" src="https://avatars.githubusercontent.com/INAH-PAK " width="80" />            
              </a>
          </td>
      </tr>
      <tr>
          <td align="center">서강휘</td>
          <td align="center">박규림</td>
          <td align="center">김현국</td>
          <td align="center">한혜원</td>
          <td align="center"> 박인아</td>
      </tr>
  </table>
</div>

## 박규림
- 담당한 일
	- Base Architecture 구조 설계
- 기여한 점
	- Clean Architecture 설계
	- Kobis, Omdb API 연동
	- Hilt 연동 

## 기술 스택 비교
### 의존성 주입 라이브러리 (Hilt vs Koin vs Dagger)
- **Koin**
	- 장점
		- Kotlin 개발 환경에 도입하기 쉬움
		- 별도의 Annotation을 사용하지 않기 때문에 컴파일 시간 단축
	- 단점
		- 런타임에 주입을 하는 방식인 Service Locator 패턴 사용 -> 퍼포먼스 떨어짐
			- Service Locator 패턴?
				- 중앙 등록자 Service Locator를 통해 요청이 들어왔을 때, 특정 인스턴스 반환
		- 런타임 시 주입이 필요한 컴포넌트가 생성이 되어있지 않은 파라미터가 있는 경우, 크래시 발생 
		- reflection을 이용하기 때문에 성능 상 좋지 않음
			- reflection?
				- 컴파일 타임에 클래스나 메소드 명을 알지 못하더라도 런타임에 타입, classpath를 이용하여 인스턴스, 객체의 상태, 메서드 정보 등을 가져올 수 있도록 지원하는 API

- **Dagger2**
	- 장점
		- 컴파일 타임에 주입에 대한 검증을 마침
	- 단점
		- 큰 러닝커브 	
		- ApplicationComponent와 ActivityComponent를 개별적으로 생성하고 각 코드 컴포넌트마다 연결을 도울 Builder를 정의하는 보일러 플레이트 코드 발생 

- **Hilt**
	- 장점
		- 컴파일 타임에 주입에 대한 검증을 마침
		- 단순화된 구성으로 프로젝트 설정 간소화, 모듈 탐색과 통합이 쉬움

<img width="621" alt="스크린샷 2022-10-06 오후 9 52 05" src="https://user-images.githubusercontent.com/31344894/194360934-ee1b9384-a29c-4c23-bd43-4fabf06d3ab2.png">


### 의존성 주입 라이브러리 => Hilt 사용 
<img width="619" alt="스크린샷 2022-10-07 오전 12 41 53" src="https://user-images.githubusercontent.com/31344894/194357831-b1305303-5ee6-46b8-9d73-eb17553571a3.png">

-----  

### HTTP 통신 라이브러리 (OkHttp3 vs Retrofit vs Volley)
- **Volley**
	- 특징
		- 이미지 캐시
		- 요청에 우선순위 부여 
		- 역/직렬화를 직접 세팅해줘야함

- **OkHttp3**
	- 특징
		- 반환받은 Json 객체 → 데이터 클래스 변환 불가
			- 별도의 과정을 통해 직접 변환
		- 네트워크 호출은 백그라운드에서 수행이 되지만, 응답값도 백그라운드에 있기 때문에 응답값으로 UI 업데이트가 이루어져야한다면 메인 스레드로 보내주는 작업 필요 

- **Retrofit**
	- 특징
		- type-safe한 HTTP 클라이언트 라이브러리
			- type safe? 
				- 네트워크로부터 전달된 데이터를 프로그램에서 필요한 형태의 객체로 받을 수 있다는 의미 
		- Gson Converter Factory를 사용하면 응답 객체의 body를 별도 변환없이 바로 사용 가능
		* 네트워크 호출의 응답값을 메인 스레드에서 사용 가능
		* 어노테이션 사용으로 코드의 가독성이 좋고 직관적인 설계 가능

<img width="807" alt="스크린샷 2022-10-06 오후 6 30 34" src="https://user-images.githubusercontent.com/31344894/194361932-cfcb0e7b-62a8-48c4-aaac-2fe138fff39a.png">

### HTTP 통신 라이브러리 => Retrofit 선택 
<img width="746" alt="스크린샷 2022-10-07 오전 12 44 09" src="https://user-images.githubusercontent.com/31344894/194358403-005056f8-99b8-4ef7-93d7-53df3d85bb14.png">

-----  

### HTTP 통신 시 역/직렬화 라이브러리 (Gson vs Moshi vs Kotlinx Serialization)
- **Gson**
	* not null한 변수에 null 값이 들어갈 수 있음 → 런타임 오류 발생 가능성
	* default value를 무시하고 0 또는 null로 역/직렬화하는 문제점
	* reflection 방식 사용하여 Json string을 역/직렬화
- **Moshi**
	* default value를 무시하고 0 또는 null로 역/직렬화하는 문제점
- **Kotlinx Serialization**
	* 잘못 작성된 코드는 컴파일 에러로 잡힘 → 컴파일 안전을 보장
	* reflection을 사용하지 않아 성능적인 장점 존재

	<img width="694" alt="스크린샷 2022-10-06 오후 10 34 51" src="https://user-images.githubusercontent.com/31344894/194361493-5f99a744-8e55-4c52-9ad9-7177a065eb83.png">  

	- Kotlinx Serialization 사용할 시 속도 향상 정도 

### HTTP 통신 시 역/직렬화 라이브러리 => Gson 선택
<img width="682" alt="스크린샷 2022-10-07 오전 12 47 13" src="https://user-images.githubusercontent.com/31344894/194359067-be0b6e13-36bc-419f-a4e3-b692fa269a42.png">  

- Gson 보다는 Kotlinx Serialization의 성능이 더 좋았으나, 익숙함을 사유로 Gson을 선택

-----  

### Image 라이브러리 (Glide vs Picasso vs Fresco vs Coil)
- **Picasso**
	- 장점
		- 메모리를 많이 사용하지 않는 경우 적합
			- Picasso 2.5.1 vs Glide 3.5.2
			<img width="798" alt="스크린샷 2022-10-07 오전 12 24 57" src="https://user-images.githubusercontent.com/31344894/194359560-2621e2ab-7cb2-427a-bdda-fffd7964685c.png">  

	- 단점
		- 많은 고용량 이미지 처리에 부적합 
- **Fresco**
	- 단점
		- 높은 러닝커브 
- **Glide**
	- 장점
		- 로딩 속도가 Picasso 보다 빠름 
		- gif 지원 
		- OkHttp 라이브러리에 연결할 수 있는 유틸리티 라이브러리가 포함되어 있어, 라이브러리와 호환성이 좋음
		- 이미지 뷰의 크기를 측정한 다음 원본 이미지를 가져와 이미지 뷰 크기에 맞게 리사이징 후 비트맵에 그려주기 때문에 메모리 효율성이 좋음
	- 단점
		- 메모리 부담 존재 
- **Coil**
	- 장점
		- Glide, Fresco 보다 상대적으로 가벼움
		- 메모리와 디스크의 캐싱, 메모리의 이미지 다운 샘플링, Bitmap 재사용 등 최적화 작업을 통해 처리 속도가 빠름
		- ImageView의 확장함수로 지원하고, 코틀린으로 작성되었기에 다른 라이브러리보다 간결한 코드 구성 가능 
	- 단점
		- Coroutine 개념 선행 필요
	
=> 빠른 로딩 속도를 위한 Glide와 처리 속도가 빠른 coil 사용 

## Clean Architecture 
<img width="519" alt="스크린샷 2022-10-06 오후 10 59 44" src="https://user-images.githubusercontent.com/31344894/194359965-720b5e68-81ef-4479-95ad-321c3e445e2c.png">

- Presentation
	- UI와 관련된 작업을 담당하는 Layer로 구성되어 있습니다.
	- Activity, ViewModel

- Domain
	- 비지니스 로직에서 수행되어져야할 행동을 정의하고 이를 interface로 제공합니다.
		- Repository, UseCase 

- Data
	- Kobis, Omdb API 요청을 수행합니다. 
	- Domain에서 제공하는 인터페이스를 확장하는 클래스로 구성합니다. 

## UseCase
- UseCase를 통해 Repository에서 접근할 수 있는 부분을 세부적으로 분리시켰습니다. 
<img width="1675" alt="스크린샷 2022-10-06 오후 11 31 39" src="https://user-images.githubusercontent.com/31344894/194360055-fb3b60b8-da78-4d21-b426-94ae62b0b3e8.png">


## Schema
### DailyBoxOffice
- 박스오피스 순위 정보

|변수명|정보|
|--|--|
|boxOfficeType|박스오피스 종류|
|showRange|박스오피스 조회 일자|
|rank|해당일자의 박스오피스 순위|
|rankInten|전일대비 순위의 증감분|
|rankOldAndNew|랭킹에 신규진입여부|
|movieCd|영화의 대표코드|
|movieNm|영화명(국문)|
|openDt|영화의 개봉일|
|audiCnt|해당일의 관객수|
|audiAcc|누적관객수|

### MovieInfos
- 영화 상세 정보 

|변수명|정보|
|--|--|
|movieCd|영화의 대표코드|
|movieNm|영화명(국문)|
|movieNmEn|영화명(영문)|
|movieNmOg|영화명(원문)|
|prdtYear|제작연도|
|showTm|상영시간|
|openDt|개봉연도|
|genres|장르|
|directors|감독|
|actors|배우|
|audits|관람등급|

### PosterInfo
- 영화 포스터 이미지

|변수명|정보|
|--|--|
|Title|영화 이름|
|Poster|영화 포스터 이미지|

### API Interface
- Kobis와 Omdb에서 영화 정보들을 가져옵니다. 

<img width="765" alt="스크린샷 2022-10-06 오후 11 36 27" src="https://user-images.githubusercontent.com/31344894/194363788-754ab70d-3f76-462e-99c4-efa03c1d6059.png">


# 일일 박스 오피스 Screen - 김현국

## 구현
<img src="https://user-images.githubusercontent.com/62296097/194360182-702faf1f-3580-47fa-a0bb-dee531aa1cbd.gif" width="300" height="600" />

## 데이터 로드 로직
```kotlin
private fun getBoxOfficeList(key: String, date: String, code: String) {
        viewModelScope.launch {
            val result = dailyBoxOfficeUseCase.getDailyBoxOfficeList(key, date, code)
            if (result?.boxOfficeResult != null) {
                // 첫번째로 영화 정보 가져오기 
                _dailyMovieBoxList.value = result.boxOfficeResult.dailyBoxOfficeList.map {
                    it.asModel()
                }
                
                result.boxOfficeResult.dailyBoxOfficeList.forEachIndexed { index, data ->
                    launch {
                        //launch를 이용하여 병렬처리
                        val response = movieInfosUseCase.getMovieInfo(
                            key = "d78dfcf081301ea1719d6d8d36756527",
                            movieCd = data.movieCd
                        )
                        // 영화의 영어이름을 가져옵니다. 
                        if (response != null) {
                            val poster = posterInfoUseCase.getPosterInfo(
                                response.movieInfoResult.movieInfo.movieNmEn,
                                key = "fa8d1585"
                            )

                            _dailyMovieBoxList.value = _dailyMovieBoxList.value.map { boxOffice ->
                                if (boxOffice.movieCd == data.movieCd) {
                                    // map으로 접근하는 movieCd와 위의 for문의 index가 같다면,
                                    // 포스터 정보를 업데이트 해주고, 
                                    //이미지 로드가 되었다는 flag인 isReady 를 true로 변경합니다.
                                    boxOffice.copy(
                                        moviePoster = poster?.Poster ?: "",
                                        isReady = true
                                    )
                                } else {
                                    boxOffice
                                }
                            }
                        }
                    }
                }
            }
        }
    }
```

## 데이터 분기처리
```kotlin
// In LazyColumn == RecyclerView
stickyHeader {}
if (data.isNotEmpty()) {
 	itemsIndexed(
           items = data,
           key = { _, boxOffice ->
                    boxOffice.ranking
           }
) { index, boxOffice ->
    when (index) {
        data.lastIndex -> {
         //BoxOfficeItem Composable
        }
        0 -> {
         //BoxOfficeItem Composable
        }
        else -> {
         //BoxOfficeItem Composable
        }
}
else{
    items(
        items = DUMMY_LIST,
        key = {
            it.movieCd
        }
        ) {
            DummyBoxOfficeItem()
        }
}
```

LazyColumn에 content Padding을 줄 수 있었지만, stickHeader에서도 padding이 생겨서 index에 따른 분기처리와

데이터가 없다면 Dummy 컴포저블 리스트가 보여지도록 하였습니다.

## 아이템 클릭처리
```kotlin
Row(
    modifier = Modifier
        .fillMaxWidth()
        .height(150.dp)
        .clickable(
            interactionSource = interactionSource,
            indication = null
        ) {
            if (boxOffice.isReady) {
                onClick(boxOffice)
            }
    },
    //
```
<p>viewModel에서 이미지를 로드를 했을때 이미지가 없는 것을 확인을 했거나, url이 들어왔을 경우 
isReady 를 true를 해줌으로써,</p>
<p>
이미지가 있는 상태로 intent를 날려줄 수 있도록 처리했습니다. 
</p>
indication은 아이템 클릭시의 effect를 보여주는데, 이미지가 로드가 되지 않았을때

클릭이 되는 effect가 발생한다면, 오류로 판단될 수도 있을 것 같아서 클릭 effect를 제거하였습니다.

## 이미지 순위 표시
<img src="https://user-images.githubusercontent.com/62296097/194359726-a35763c9-8601-44c7-9429-b060ef32eb7b.jpeg">

```kotlin
// 코드 생략
SubcomposeAsyncImage() // 이미지 컴포저블
Box(
    modifier = Modifier.fillMaxSize().align(Alignment.BottomCenter).background(
    brush = Brush.verticalGradient( // 이미지의 그라디언트 처리
        listOf(
            Color(0x00E4E8F5),
            Color(0xFF788098)
        )
    ),
        shape = RoundedCornerShape(5.dp)
    )
    ) {
        Box(modifier = Modifier.padding(start = 3.dp).align(Alignment.BottomStart)) {
            Text(
                text = boxOffice.ranking,
                //
            )
        }
        if (boxOffice.rankType == "NEW") {
            Box(
                modifier = Modifier.align(Alignment.BottomEnd)
            ) {
                Text(
                    text = boxOffice.rankType,
                    //
                )
            }
        }
    }
```
포스터의 배경이 흰색이여도 순위가 잘보여지게 하기 위해서, 이미지 컴포저블에 그라디언트를 겹쳐서 표현했습니다.

또한 영화가 새롭게 진입한 영화라면, New Text가 보여지도록 구현하였습니다.

## 한혜원
- 담당한 일
	- 두번째 페이지 구현
- 기여한 점
	- 영화 상세 정보
	- 리뷰 목록 
	- 영화 상세 정보 공유
- 남은 일
	- 리뷰 목록 구현
	- ui에 motionlayout 적용해보기
- 실행영상

https://user-images.githubusercontent.com/35549958/194384816-9052d7da-ad72-48af-ac88-157f393171cd.mp4


## Firebase 리뷰 Screen - 박인아

- 담당한 일
	- 세번째 페이지 구현
- 기여한 점
	- Firebase FireStore 연동
	- 리뷰 목록 
	- 리뷰 작성 페이지 구현
- 남은 일
	- Hilt 적용
	- Coroutine 적용
	- FirebaseFirestore 싱글톤 구현
	- viewBinding 을 DataBinding으로 변경
	- 사진 업로드 구현
	

## Realtime Database vs Cloud Firestore

<div align="center">
  <table style="font-weight : bold">
      <tr>
          <td align="center">Realtime Database</td>
          <td align="center">Cloud Firestore</td>
      </tr>
      <tr>
          <td align="center"><img src="https://user-images.githubusercontent.com/95750706/194424517-d32bb3c5-7b9b-4824-b221-0437bec0fcf5.png" width="400"  /></td>
          <td align="center"><img src="https://user-images.githubusercontent.com/95750706/194425932-2372939c-8ad7-4d55-806a-1041775e4033.png" width="400"  /></td>
      </tr>
  </table>
</div>


- Realtime Database
	- 데이터를 하나의 큰 JSON 트리로 저장함.
	- 쿼리시, 정렬과 필터링만 가능하며, 기본적으로 해당 depth의 데이터 반환시 그 이하의 모든 depth가 반환됨. -> 성능저하 발생 가능
- Cloud Firestore
	- 데이터가 문서와 컬렉션으로 이루어짐.
	- 쿼리시, 정렬과 필터링 조건문을 동시 사용 가능하며, 쿼리가 얕아서 특정 컬렉션이나 컬렉션의 문서만 반환 됨. -> 성능저하 발생 가능성 낮음
	- Realtime Databas의 여러 단점들 보완 및 성능 개선되어 출시됨.
	
<p>
구조화된 데이터 구성을 원하여 Cloud Firestore 를 선택.
</p>


## Android MVVM 패턴

<img src="https://user-images.githubusercontent.com/95750706/194421297-dfcbbf74-045f-497e-811f-d3d29ef2d890.JPG" width="400"  />

## Firebase의 Android MVVM 패턴
<img src="https://user-images.githubusercontent.com/95750706/194420307-2840a55f-7c2a-46c9-9e0c-34371be39641.JPG" width="400"  />

<p>
FireStore는 자체적으로 로컬 캐시를 적용하므로, 기존의 MVVM 패턴에서 쓰이는 모델과 원격 데이터 소스를 제거한 단일 레포지토리 클래스로 결합함.
</p>

 - 데이터 구성
![miri1](https://user-images.githubusercontent.com/95750706/194430597-3bfa5401-34c6-476b-b081-a04becca9301.png)


 - Model
 ```kotlin
data class ReviewVO(
    val contents:String = "",
    val imageUrl:String = "",
    val movie_id:String = "",
    val name:String = "",
    val password:String = "",
    val time: Timestamp  = Timestamp.now(),
    val star: Int = 404
)

```
 - Repository
 	- FireStore 데이터베이스에서 리뷰 저장, 가져오기에 대한 액세스 권한을 만듬.
 	- 데이터 저장시, 커스텀 클래스(ReviewVO)를 사용하여 문서를 작성.
 
 ```kotlin

    fun saveReviewItem(review: ReviewVO): Task<Void> {
        //var
        var documentReference = firestoreDB.collection("reviews").document(review.movie_id)
            .collection(review.movie_id).document()
        return documentReference.set(review)
    }

    fun getSavedReview(movieCd: String): CollectionReference = firestoreDB.collection("reviews").document(movieCd).collection(movieCd)


```

 - ViewModel
 	- 리뷰 데이터를 관리함.
 	- 여러 사용자들의 리뷰가 달리므로, 데이터가 변경되는 순간 데이터를 받아와 UI를 업데이트 하기위해, Push Driven 방식으로 firebase의 리뷰들을 가져옴.
 	- 
 
 ```kotlin
 class ReviewViewModel() : ViewModel() {
    val TAG = "FIRESTORE_VIEW_MODEL"
    var firebaseRepository = FirestoreRepository()
    var savedReviews : MutableLiveData<List<ReviewVO>> = MutableLiveData()
 	

    // save review to firebase
    fun saveReviewToFirebase(review: ReviewVO){
        firebaseRepository.saveReviewItem(review).addOnFailureListener {
            Log.i(TAG,"Failed to save Address!")
        }
    }
    
    fun getReviews(){
	firebaseRepository.getSavedReview("20112207").addSnapshotListener(EventListener<QuerySnapshot>{ value, e ->
            if (e != null) {
                return@EventListener
            }
            var savedReviewList : MutableList<ReviewVO> = mutableListOf()
            for (doc in value!!) {
                var reviewItem = doc.toObject(ReviewVO::class.java)
                savedReviewList.add(reviewItem)

            }
            reviews = savedReviewList
        })
        binding.recycler.adapter!!.notifyDataSetChanged()
	}
     }

```

 - View
  
 <img src="https://user-images.githubusercontent.com/95750706/194432866-a0fcd087-367e-4e23-8d11-32aab0beb44b.jpg" width="300"  /> <img src="https://user-images.githubusercontent.com/95750706/194432874-60af44df-1a33-4f7d-b43f-22623206d304.jpg" width="300"  />



## Convention

### Branch Convention

``` issue-<issue Number>/<branch name>  ```

- e.g) ``` issue-#1/Base Architecture ```


### Commit convention

``` [prefix]: <commit content> ```

- e.g) ``` feat: DAO 개발완료 ```

- e.g) ``` fix: room crash 수정 ```

- e.g) ``` refactor: MVVM 아키텍처 구조 리팩토링 ```

### Issue Convention
``` [prefix] 작업할 내용 ```

- e.g) ``` [feat] base architecture 생성 ```
- e.g) ``` [fix] room crash 수정 ```
- e.g) ``` [refactor] Sensor구조 일부 수정 ```

- 브랜치를 생성하기 전, github issue를 생성해주세요.
- branch 명의 issue number는 해당 issue Number로 지정합니다.

### PR Convention
``` [Issue-#number] PR 내용 ```

- e.g) ``` [Issue-#7] Timer 추가 ``` 

-----
### 출처 
- https://mashup-android.vercel.app/mashup-12th/jieun/kotlinx-serialization/
- https://gun0912.tistory.com/19
- http://instructure.github.io/blog/2013/12/09/volley-vs-retrofit/
- https://blog.banksalad.com/tech/migrate-from-koin-to-hilt/
