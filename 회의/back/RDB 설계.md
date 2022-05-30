# RDB 설계

#### 회원가입

- User TB
  - 주소 => 물품 TB에 JOIN
- Region TB
  - 테이블의 지역 데이터는 더미 데이터를 넣는 것으로(군구동)



#### 물품 게시판

- Stuff(예명) TB
  - 주소 == User의 주소
  - 컬럼 : 
  - title(제목)
  - content(상품 설명)
  - img(상품 이미지)
  - prise(가격)
  - ggleorle(끌올)
    - 버튼을 누르면 끌올 count++해서 updateDate 오늘날짜로 수정하기, 조건에 따라서 이상이 되면 더 이상 못하게 막기
- User TB (JOIN)
- Category TB (JOIN)
- like TB (JOIN)
- chat TB (JOIN)
- Views TB (JOIN)



#### 동네생활

1. 게시글 리스트

- Category TB
  - Content(내용)
  - 궁금해요, 공감하기(질문 빼고 다)
  - 답변, 댓글(질문 빼고 다)
  - User TB, Users's Region
  - Post의 CreateDate
  - 썸네일
- Like TB

2. 게시글 상세보기
   1. 댓글 기능(Comment TB)
      1. 좋아요, 답글쓰기
      2. User TB JOIN, User's Region
      3. CreateDate
      4. 작성자가 댓글을 쓰면 프로필 옆에 작성자라는 박스가 생김
3. 글쓰기
   1. User TB
   2. Post TB
      1. content
      2. Title
      3. 지역 기능
   3. Category TB



### RDB 관계 설정

1. User TB
   1. id
   2. phone number
   3. email
   4. username
   5. region
   6. manaer
   7. profile img
   8. postId
   9. likeId
   10. stuffId
   11. chatId
   12. managerId
   13. reviewId
   14. createDate
   15. updateDate
2. Post(동네생활만) TB
   1. 동네생활
      1. id
      2. content
      3. categoryId
      4. userId
      5. commentId
      6. likeId
      7. thumbnail
      8. createDate
      9. updateDate
3. Category(물품 게시판, 동네생활) TB
   1. 물품 게시판
      1. id
      2. name
      3. createDate
      4. updateDate
   2. 동네생활
      1. id
      2. name
      3. createDate
      4. updateDate
4. Like(물품 게시판, 동네생활) TB
   1. 물품 게시판
      1. id
      2. count
      3. userId
      4. stuffId
      5. createDate
      6. updateDate
   2. 동네생활
      1. id
      2. count
      3. userId
      4. postId
      5. createDate
      6. updateDate
5. View(물품 게시판, 동네생활) TB
   1. 물품 게시판
      1. id
      2. count
      3. userId
      4. postId
      5. createDate
      6. updateDate
   2. 동네생활
      1. id
      2. count
      3. userId
      4. postId
      5. createDate
      6. updateDate
6. Stuff(물품 게시판) TB
   1. 물품 게시판
      1. id
      2. title
      3. content
      4. thumbnail
      5. categoryId
      6. userId(판매자, 구매자)
      7. likeId
      8. viewId
      9. prise
      10. chatId
      11. createDate
      12. updateDate
      13. 판매중과 거래완료는 0, 1로 나누기
7. Chat(채팅 페이지만) TB
   1. id
   2. userId(보내는 사람, 받는 사람)
   3. chatting(채팅 내용)
   4. Img
   5. stuffId
   6. createDate
   7. updateDate
8. Manager(받은 매너 평가) TB
   1. id
   2. keyword
   3. number
   4. userId
   5. createDate
   6. updateDate
9. Review(받은 거래 후기) TB
   1. id
   2. content
   3. userId
   4. stuffId
   5. createDate
   6. updateDate

#### 관계



#### 동네찾기 할 때 지오로케이션 사용에 대해서

1. 테이블을 만들어서 셀렉을 하는 게 아니라 지오로케이션으로 사용자의 위치를 알고 이를 통해서 프론트에 동네까지만 걸러서 화면에 뿌리도록 하자.
2. 이건 자바스크립트를 써야 하기 때문에 프론트에서 작업하도록 한다.
3. 지오로케이션은 사용자의 컴퓨터 위치를 뽑아서 x, y 좌표로 출력한다.