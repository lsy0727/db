# db

### pymongo 라이브러리에서 mongodb와 통신하기 위한 MongoClient 클래스를 가져옴
from pymongo import MongoClient

### 27017 포트에서 실행 중인 로컬 mongodb 서버에 연결
client = MongoClient('mongodb://localhost:27017/')

### LOL-2024 데이터베이스에 접근
db = client['LOL-2024']

### LOL-2024 데이터베이스 안에서 team이라는 이름의 컬렉션에 접근
collection = db['team']

### 임의의 문서 10개 동시 삽입(insert_many)
### result = collection.insert_many([   ### 문서 삽입
###     {
###         "리그" : "LCK",
###         "팀이름" : "T1",
###         "감독" : "김정균",
###         "코치" : "임재현",
###         "선수" : ["Zzeus", "Oner", "Faker", "Gumayusi", "Keria"] ### top, jg, mid, ad, sup 순서서
###     },
###     {
###         "리그" : "LCK",
###         "팀이름" : "Gen.G",
###         "감독" : "김정수",
###         "코치" : ["조세형", "권영재"],
###         "선수" : ["Kiin", "Canyon", "Chovy", "Ruler", "Pekez/Su-hwan"]
###     },
###     {
###         "리그" : "LCK",
###         "팀이름" : "KT Rolster",
###         "감독" : "강동훈",
###         "코치" : "강동훈",
###         "선수" : ["PerfecT", "Cuzz", "Bdd", "deokdam", "Peter"]
###     },
###     {
###         "리그" : "LCK",
###         "팀이름" : "Dplus KIA",
###         "감독" : "이재민",
###         "코치" : ["박준형", "김상수"],
###         "선수" : ["Siwoo", "Lucid", "ShowMaker", "Aiming", "BeryL"]
###     },
###     {
###         "리그" : "LCK",
###         "팀이름" : "Hanwha Life Esports",
###         "감독" : "최인규",
###         "코치" : ["이재하", "신동욱"],
###         "선수" : ["Doran", "Peanut", "Zeka", "Viper", "Delight"]
###     },
###     {
###         "리그" : "LPL",
###         "팀이름" : "Invictus Gaming",
###         "감독" : "Zhu Xiao‑Long",
###         "코치" : "Zhu Xiao-Long",
###         "선수" : ["YSKM", "Tianzhen", "Cryin", "Ahn", "Wink"]
###     },
###     {
###         "리그" : "LPL",
###         "팀이름" : "JD Gaming",
###         "감독" : "Won Sang‑yeon",
###         "코치" : "Won Sang‑yeon",
###         "선수" : ["sheer", "Kanavi", "Yagao", "Ruler", "MISSING"]
###     },
###     {
###         "리그" : "LPL",
###         "팀이름" : "LGD Gaming",
###         "감독" : "Chen Li‑Xin",
###         "코치" : "Chen Li‑Xin",
###         "선수" : ["Burdol", "Meteor", "Haichao", "Kepler", "TBA"]
###     },
###     {
###         "리그" : "LEC",
###         "팀이름" : "Fnatic",
###         "감독" : "Fabian Lohmann",
###         "코치" : ["GrabbZ", "Gaax"],
###         "선수" : ["Oscarinin", "Razork", "Humanoid", "Noah", "Jun"]
###     },
###     {
###         "리그" : "LEC",
###         "팀이름" : "G2 Esports",
###         "감독" : "Dylan Falco",
###         "코치" : "Dylan Falco",
###         "선수" : ["BrokenBlade", "Yike", "Caps", "Hans Sama", "Mikyx"]
###     }
### ])


### 하나의 필드를 이용해 중복 삽입 방지 인덱스 추가(create_index)
### from pymongo.errors import DuplicateKeyError    ### pymongo 라이브러리에서 DuplicateKeyError 예외 클래스를 가져옴

### result = collection.create_index(   ### 중복방지 인덱스 (result)
###     "팀이름",   ### 팀이름에 대해 고유 인덱스 생성
###     unique=True ### 이 인덱스를 통해 같은 팀 이름으로 문서를 두 번 이상 삽입하면 오류 발생함함
### )   ### 반환값 result : 생성된 인덱스의 이름
### try:
###     result = collection.insert_one({    ### mongodb에 문서 삽입
###         "리그" : "LCK",
###         "팀이름" : "Dplus KIA", ### "팀이름" 필드에 "Dplus KIA" 지정되어있음 -> 기존 필드에 존재하면 DuplicateKeyError 발생생
###         "감독" : "이재민",
###         "코치" : ["박준형", "김상수"],
###         "선수" : ["Siwoo", "Lucid", "ShowMaker", "Aiming", "BeryL"]
###     })
###     print(f"문서 삽입 결과 : {result}") ### 중복되지 않을 시 결과 출력
### except DuplicateKeyError:   ### try 블럭 내에서 중복 키 예외 발생 시
###     print("중복된 팀입니다")    ### 중복 메시지 출력


### 임의의 문서 3개를 추가로 삽입(insert_many or insert_one)
### result = collection.insert_many([   ### 문서삽입
###     {
###         "리그" : "LPL",
###         "팀이름" : "Bilibili Gaming",
###         "감독" : "Maokai",
###         "코치" : ["LvMao", "Easyhoon"],
###         "선수" : ["Bin", "XUN", "knight", "Elk", "ON"]
###     },
###     {
###         "리그" : "LPL",
###         "팀이름" : "Top Esports",
###         "감독" : "Homme",
###         "코치" : ["Ggoong", "Ben"],
###         "선수" : ["369", "Kanavi", "Creme", "JackeyLove", "Crisp"]
###     },
###     {
###         "리그" : "LPL",
###         "팀이름" : "LNG Esports",
###         "감독" : "Viod",
###         "코치" : "-",
###         "선수" : ["Zika", "Weiwei", "Scout", "GALA", "Hang/Mark"]
###     }
### ])


### 컬렉션 내의 모든 문서 출력(find)
### for t in collection.find(): ### 컬렉션 내의 모든 문서
###     print(t)    ### 문서 내용 출력


### 컬렉션 내에서 특정 조건을 만족하는 문서 전부 출력(find)
### team_find = collection.find({   ### team_find = 문서를 찾아서 저장
###     "팀이름" : "T1" ### 팀이름이 T1인 문서
### })
### for t in team_find: ### 문서 내의 모든 내용
###     print(t)    ### 출력


### 컬렉션 내에서 특정 조건을 만족하며, 특정 필드를 기준으로 오름차순or내림차순 정렬하여 출력(sort)
### team_sort = collection.find({   ### 컬렉션 내에서 특정 조건을 만족하는 문서 검색
###     "리그" : "LCK"  ### "리그" 가 "LCK"인 문서
### }).sort("팀이름", 1)    ### "팀이름" 필드를 기준으로 오름차순 정렬
### for t in team_sort: ### 정렬된 문서들
###     print(t)    ### 출력


### 특정 문서의 필드값 변경(update_one)
### collection.update_one(  ### 필드 값 변경
###     {"팀이름" : "T1"},  ### 팀이름이 T1인 문서에서
###     {"$set" : {"선수.0": "zeus"}}   ### 선수 배열의 0번 인덱스 값을 zeus로 변경
### )
### team_update = collection.find(  ### 컬렉션 내에서 검색
###     {"팀이름" : "T1"}   ### 팀이름이 T1인 문서
### )
### for t in team_update:   ### 팀이름이 T1인 문서의 모든 내용
###     print(t)    ### 출력


### 모든 문서의 필드명 변경(update_many)
### collection.update_many( ### 필드 값 변경
###     {}, ### 모든 문서
###     {
###         "$rename" : {"감독" : "헤드코치"} ### 감독 -> 헤드코치로 변경
###     }
### )
### team_update_many = collection.find()    ### 컬렉션 내에서 검색
### for t in team_update_many:  ### 컬렉션 내의 모든 문서
###     print(t)    ### 출력


### 특정 조건을 만족하는 문서 1개 삭제(delete_one)
### result_delete_one = collection.delete_one({   ### 문서 제거
###     "감독" : "Zhu Xiao‑Long"  ### 감독이 Zhu Xiao‑Long인 문서
### })
### print(result_delete_one)  ### 결과 n:1, ok:1.0, acknowledged=True가 나오면 성공(n: 삭제된 문서수, ok: 1.0-성공/0-실패, True: 명령을 정상적으로 수행)



### ### 조건 없이 2개의 문서 삭제(delete_many)
### delete_find = collection.find().limit(2)  ### 조건 없이 2개의 문서 검색
### delete_list = [doc["_id"] for doc in delete_find]   ### 해당 문서들의 _id값을 추출해 리스트 생성
### result_delete_many = collection.delete_many({"_id" : {"$in" : delete_list}})    ### 해당 문서 제거
### print(result_delete_many)   ### 결과 n:2, ok:1.0, acknowledged=True가 나오면 성공(n: 삭제된 문서수, ok: 1.0-성공/0-실패, True: 명령을 정상적으로 수행)


### ### 특정 조건을 만족하는 문서 2개 삭제(delete_many)
### result_delete_many2 = collection.delete_many({ ### 문서 제거
###     "$or" : [     ### 조건
###         {"감독" : "Maokai"},  ### 감독이름이 Maokai
###         {"팀이름" : "LNG Esports"}    ### 팀이름이 LNG Esports
###     ]
### })
### print(result_delete_many2)

### ### 모든 문서 검색
### team_update_many = collection.find()    ### 컬렉션 내에서 검색
### for t in team_update_many:  ### 컬렉션 내의 모든 문서
###     print(t)    ### 출력
