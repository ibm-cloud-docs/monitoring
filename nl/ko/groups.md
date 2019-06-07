---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, groups

subcollection: Sysdig

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}
{:important: .important}
{:note: .note}

# 그룹 관리
{: #groups}

레이블을 사용하여 인프라 오브젝트를 논리적 계층 구조로 그룹화할 수 있습니다.
{:shortdesc}

## 그룹 작성
{: #create_group}

그룹을 작성하려면 다음 단계를 완료하십시오.

1. 웹 UI를 실행하십시오. [자세히 보기](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 

2. **탐색**을 클릭하여 *탐색* 섹션으로 이동하십시오.

3. **탐색 테이블로 돌아가기**를 선택하십시오.

4. *더하기(+)* 아이콘을 클릭하여 레이블을 더 추가할 수 있습니다.

    레이블을 추가하면 올바른 논리적 그룹화만 작성되도록 계층 구조에 맞지 않는 레이블이 필터링되어 걸러집니다.
    {: tip}

5. 레이블 추가가 완료되면 **새 그룹화**를 클릭하십시오.

6. **현재 그룹화 저장**을 선택하십시오.

7. 작성할 그룹의 이름을 입력하십시오.

8. *확인* 아이콘 ![확인 아이콘](images/ok.png)을 클릭하십시오.

## 그룹 이름 바꾸기
{: #rename_group}

그룹 이름을 바꾸려면 다음 단계를 완료하십시오.

1. 웹 UI를 실행하십시오. [자세히 보기](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 

2. **탐색**을 클릭하여 *탐색* 섹션으로 이동하십시오.

3. 호스트 전환 아이콘 ![호스트 전환 아이콘](images/switch_hosts.png)을 클릭하십시오.

4. 그룹을 선택하십시오.

5. 조치 아이콘 ![세 점 아이콘](images/actions.png)을 클릭하고 **그룹화 조치 표시**를 선택하십시오.

6. 편집 아이콘 ![연필 아이콘](images/edit.png)을 선택하십시오.

7. 새 이름을 입력하십시오.

8. *확인* 아이콘 ![확인 아이콘](images/ok.png)을 클릭하십시오.




## 그룹 복사
{: #copy_group}

기타 팀으로 그룹을 복사하려면 다음 단계를 완료하십시오.

1. 웹 UI를 실행하십시오. [자세히 보기](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 

2. **탐색**을 클릭하여 *탐색* 섹션으로 이동하십시오.

3. 호스트 전환 아이콘 ![호스트 전환 아이콘](images/switch_hosts.png)을 클릭하십시오.

4. 그룹을 선택하십시오.

5. 조치 아이콘 ![세 점 아이콘](images/actions.png)을 클릭하고 **그룹화 조치 표시**를 선택하십시오.

6. 그룹 복사 아이콘 ![복사 아이콘](images/copy.png)을 선택하십시오.

7. *복사 대상* 필드에서 이 그룹을 복사할 팀을 선택하십시오.

8. 다른 이름으로 그룹을 복사하려면 *이름* 필드에서 새 그룹 이름을 입력하십시오.

9. **사본 전송**을 클릭하십시오.



## 그룹 공유
{: #share_group}

팀의 기타 구성원과 그룹을 공유하려면 다음 단계를 완료하십시오.

1. 웹 UI를 실행하십시오. [자세히 보기](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 

2. **탐색**을 클릭하여 *탐색* 섹션으로 이동하십시오.

3. 호스트 전환 아이콘 ![호스트 전환 아이콘](images/switch_hosts.png)을 클릭하십시오.

4. 그룹을 선택하십시오.

5. 조치 아이콘 ![세 점 아이콘](images/actions.png)을 클릭하고 **그룹화 조치 표시**를 선택하십시오.

6. 그룹 공유 아이콘 ![공유 아이콘](images/share.png)을 선택하십시오.

7. *팀과 공유* 필드에서 막대를 토글하여 팀의 다른 구성원과의 그룹 공유를 사용으로 설정하십시오.

8. **닫기**를 클릭하십시오.



## 그룹 삭제
{: #delete_group}

그룹을 삭제하려면 다음 단계를 완료하십시오.

1. 웹 UI를 실행하십시오. [자세히 보기](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 

2. **탐색**을 클릭하여 *탐색* 섹션으로 이동하십시오.

3. 호스트 전환 아이콘 ![호스트 전환 아이콘](images/switch_hosts.png)을 클릭하십시오.

4. 그룹을 선택하십시오.

5. 조치 아이콘 ![세 점 아이콘](images/actions.png)을 클릭하고 **그룹화 조치 표시**를 선택하십시오.

6. 그룹 삭제 아이콘 ![삭제 아이콘](images/delete.png)을 선택하십시오.

7. **예, 그룹을 삭제합니다**를 클릭하여 그룹 삭제를 확인하십시오.






