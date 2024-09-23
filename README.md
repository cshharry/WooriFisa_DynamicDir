
# 📂 동적 디렉토리 생성 & 💾 디렉토리 백업 자동화

## 📂 동적 디렉토리 생성

### 개요
사용자가 입력한 디렉토리 이름과 인덱스 범위에 따라 디렉토리를 동적으로 생성합니다. 예를 들어, 디렉토리 이름을 `fisa`로 설정하고 1에서 5까지 인덱스를 지정하면 `fisa1`, `fisa2`, `fisa3` 등의 디렉토리가 생성됩니다.

### 파일 설명
```bash
#!/bin/sh

if [ "$#" -ne 3 ]
then
    echo "디렉토리 이름, 시작 index, 끝 index 순으로 3개의 데이터 입력해 주세요"
    exit 1  # 강제종료
fi

dir_name=$1
start_number=$2
end_number=$3

for ((i=start_number; i<=end_number; i++)); 
do
    mkdir "$dir_name$i"  #fisa1   
done

echo "디렉토리 생성 완료"
```

### 사용 방법
1. 스크립트를 원하는 위치에 저장합니다.
2. 스크립트에 실행 권한을 부여합니다:

   ```bash
   chmod +x dynamic_dir_creator.sh
   ```

3. 스크립트를 실행할 때, 디렉토리 이름과 시작/끝 인덱스를 입력합니다.

   ![13](https://github.com/user-attachments/assets/e7dd3c70-873d-4b24-a4d3-ca0bb81fb06a)


### 결과
스크립트가 실행된 후에는 아래와 같이 디렉토리가 생성됩니다:

![11](https://github.com/user-attachments/assets/c16088dd-9a30-4446-aa9d-cd6d22971c43)


---

## 💾 디렉토리 백업 자동화

### 개요
**`step02shell`** 디렉토리를 매일 자동으로 백업하는 방식으로 설계하였습니다. 백업 파일은 날짜와 시간을 포함한 이름으로 저장되며, 지정된 경로에 `.tar.gz` 형식으로 압축됩니다.

### 파일 설명
```bash
#!/bin/bash

backup_file="/home/ubuntu/fisa_backup_$(date +\%Y\%m\%d_\%H\%M\%S).tar.gz"

tar -czf $backup_file /home/ubuntu/step02shell
```

- **backup_file**: 백업 파일의 이름을 현재 날짜와 시간으로 지정하여 매번 새로운 파일이 생성됩니다.
- **tar -czf**: `tar` 명령어를 사용하여 `step02shell` 디렉토리를 `.tar.gz` 형식으로 압축합니다.

### 사용 방법
1. 스크립트를 원하는 위치에 저장합니다.
2. 스크립트에 실행 권한을 부여합니다:

   ```bash
   chmod +x /home/ubuntu/step02shell/backup.sh
   ```

3. `cron`을 사용하여 이 스크립트를 매일 오전 9시에 자동으로 실행되도록 설정할 수 있습니다.

### cron 설정 방법
1. 터미널에서 다음 명령어를 실행하여 crontab을 편집합니다:

   ```bash
   crontab -e
   ```

2. 아래 줄을 추가하여 매일 오전 9시에 스크립트를 실행하도록 설정합니다:

   ```bash
   0 9 * * * /home/ubuntu/step02shell/backup.sh
   ```

3. 설정을 저장하고 crontab을 종료합니다.

### 결과
스크립트가 실행된 후 `/home/ubuntu/` 경로에 백업 파일이 생성됩니다. 파일 이름은 다음과 같이 날짜와 시간이 포함된 형식으로 저장됩니다:

![12](https://github.com/user-attachments/assets/35bb5fc1-386e-44e7-862f-4bede43e400f)
