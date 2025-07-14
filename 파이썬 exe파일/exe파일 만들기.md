## ✅ 4. 한 방에 처리하는 배치파일 (선택)


pyinstaller --noconsole --onefile --add-data "chromedriver.exe;." "가입인사 댓글.py"
pyinstaller --noconsole --onefile --add-data "chromedriver.exe;." "비제휴후기 댓글.py"
pyinstaller --noconsole --onefile --add-data "chromedriver.exe;." "자유게시판 댓글.py"
pyinstaller --noconsole --onefile --add-data "chromedriver.exe;." "후기게시판 댓글.py"