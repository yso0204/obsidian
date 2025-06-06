# **CPU 스케줄링 알고리즘의 이해: FCFS, SJF, RR**

운영체제에서 **CPU 스케줄링(CPU Scheduling)**은 여러 프로세스들이 CPU를 공정하고 효율적으로 사용할 수 있도록 순서를 정하는 중요한 작업이에요. 오늘은 대표적인 세 가지 알고리즘을 소개해볼게요!

---

## 🧾 1. FCFS (First Come First Serve)

**먼저 온 프로세스부터 처리하는 방식**이에요. 줄 서는 방식과 똑같죠!

- 📌 특징:
    
    - 구현이 간단해요.
        
    - 기다리는 시간이 길어질 수 있어요.
        
- ⛔ 단점: **Convoy Effect(호위 현상)**  
    실행 시간이 긴 작업 하나가 전체 줄을 막아버려요.
    

---

## ⏳ 2. SJF (Shortest Job First)

**실행 시간이 짧은 프로세스부터 처리하는 방식**이에요. 빨리 끝낼 수 있는 걸 먼저 처리하자는 거죠.

- 📌 특징:
    
    - 평균 대기 시간이 가장 짧음!
        
- ⛔ 단점:
    
    - 실행 시간을 미리 알아야 해요.
        
    - 긴 작업은 무한히 기다릴 수 있어요 (기아 현상, starvation)
        

---

## 🔄 3. RR (Round Robin)

**모든 프로세스에 시간 할당량(Time Quantum)을 줘서 조금씩 번갈아 가며 실행**해요.

- 📌 특징:
    
    - 공정성 높음
        
    - 인터랙티브한 시스템에 적합
        
- ⛔ 단점:
    
    - Time Quantum 설정이 너무 작으면 Overhead 증가
        
    - 너무 크면 FCFS와 다를 바 없어져요
        

---

## 💡 핵심 비교 정리

|알고리즘|방식|장점|단점|
|---|---|---|---|
|FCFS|도착 순|간단|평균 대기 시간 큼|
|SJF|짧은 작업 우선|평균 대기 시간 최소화|실행 시간 예측 필요|
|RR|일정 시간씩 할당|공정, 반응성 높음|설정이 민감|