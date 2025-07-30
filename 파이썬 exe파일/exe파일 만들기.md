## ✅ 4. 한 방에 처리하는 배치파일 (선택)


pyinstaller --noconsole --onefile --add-data "chromedriver.exe;." "가입인사 댓글.py"
pyinstaller --noconsole --onefile --add-data "chromedriver.exe;." "비제휴후기 댓글.py"
pyinstaller --noconsole --onefile --add-data "chromedriver.exe;." "자유게시판 댓글.py"
pyinstaller --noconsole --onefile --add-data "chromedriver.exe;." "후기게시판 댓글.py"

pyinstaller --onefile  --windowed "hello.py"
pyinstaller --onefile  --windowed "una.py"
pyinstaller --onefile  --windowed "free.py"
pyinstaller --onefile  --windowed "review.py"
pyinstaller --onefile  --windowed "ttest.py"
# 인스타 언팔 자동화 exe
	pyinstaller --onefile --windowed test_V2.1.py