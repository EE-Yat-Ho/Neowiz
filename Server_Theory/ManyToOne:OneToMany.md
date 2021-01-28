# ManyToOne/OneToMany
1. 쓴다
=> 삽입할 때 조인을 거쳐서 비효율
=> 쓰는거 자체가 귀찮음
=> JSON으로 그릴 때 무한참조를 끊어내는 작업을 해야함
(@JsonBackReference, @JsonManagedReference를 써주던지, 리스폰을 따로 만들던지)
=> 음.. 결론은.. 성능은 안좋을 수도 있음. 하지만 안정성과 가독성이 좋음


2. 안쓴다
=> 성능 좋음, 안정성과 가독성이 안좋음
