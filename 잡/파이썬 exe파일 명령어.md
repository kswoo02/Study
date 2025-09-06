## 4. 한 번에 처리


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
pyinstaller --onefile --windowed Instargram_Unfollow.py
pyinstaller --onefile --windowed Un_Inst_API.py
pyinstaller --onefile --windowed follower_ing.py
pyinstaller --onefile --windowed list_unfo.py
