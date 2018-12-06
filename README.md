# GitLearning
Hướng dẫn bạn học và hiểu về git 1 cách cơ bản. Thích hợp cho người mới học.
### 1. Các khái niệm cơ bản về GIT
Git là một trong những Hệ thống Quản lý Phiên bản Phân tán, vốn được phát triển nhằm quản lý mã nguồn (source code) của Linux.

Trên Git, ta có thể lưu trạng thái của file dưới dạng lịch sử cập nhật. Vì thế, có thể đưa file đã chỉnh sửa một lần về trạng thái cũ hay có thể biết được file đã được chỉnh sửa chỗ nào.

![](https://4.bp.blogspot.com/-ZYIJIZWTj-I/VTvM1dMdDCI/AAAAAAAACWA/_V9XNOLwkAw/s1600/2color-lightbg%402x.png)

Thêm nữa, khi định ghi đè (overwrite) lên file mới nhất đã chỉnh sửa của người khác bằng file đã chỉnh sửa dựa trên file cũ, thì khi upload lên server sẽ hiện ra cảnh cáo. Vì thế, sẽ không xảy ra lỗi khi ghi đè lên nội dung chỉnh sửa của người khác mà không hề hay biết.

Git sử dụng mô hình phân tán, ngược lại so với SVN hoặc CSV. Mỗi nơi lưu source sẽ đc gọi là repositories, không cần lưu trữ tập trung một nơi, mà mỗi thành viên trong team sẽ có một repository ở máy của riêng mình.
Điều đó có nghĩa là nếu có 3 người A,B,C cùng làm việc trong 1 project. Thì bản thân repo trên máy của người A, người B, và người C có thể kết nối được với nhau.

Khi quyết định thay đổi chỗ nào đó lên server ta chỉ cần một thao tác "push" nó lên server. Chúng ta vẫn có thể share thay đổi của chúng ta cho thành viên khác, bằng cách commit hoặc update trực tiếp từ máy của họ mà không phải thông qua repositories gốc trên server (thông qua share ssh cho nhau).

Lợi ích
An toàn hơn (vì mỗi bản copy của thành viên đều là full copy từ repository gốc, khi server bị down).
Các thành viên vẫn có thể làm việc offline, họ vẫn có thể commit và update trên local của họ hoặc thậm chí với nhau mà không cần thông qua server.
Khi server hoạt động trở lại, họ có thể cập nhật tất cả lên lại server.
#### a. Kho Repo (Repository)
Repository hay được gọi tắt là Repo, đơn giản là nơi chứa tất cả những thông tin cần thiết để duy trì và quản lý các sửa đổi và lịch sử của toàn bộ project. Trong Repo có 2 cấu trúc dữ liệu chính là Object Store và Index. Tất cả dữ liệu của Repo đèu được chứa trong thư mục bạn đang làm việc dưới dạng folder ẩn có tên là .git

#### b. Remote repository và local repository
Đầu tiên, repository của Git được phân thành 2 loại là remote repository và local repository.
Remote repository: Là repository để chia sẻ giữa nhiều người và bố trí trên server chuyên dụng.
Local repository: Là repository bố trí trên máy của bản thân mình, dành cho một người dùng sử dụng.
Do repository phân thành 2 loại là local và remote nên với những công việc bình thường thì có thể sử dụng local repository. Khi muốn public nội dung công việc mà mình đã làm trên local repository, thì ta sẽ upload lên remote repository rồi public. Thêm nữa, thông qua remote repository bạn cũng có thể lấy về nội dung thay đổi của người khác.
![](https://2.bp.blogspot.com/-aBPG-ztqfk0/VTvHH59jZkI/AAAAAAAACVc/eXqR_iG3oys/s1600/basic-remote-workflow.png)

#### c. Nhánh (Branch)
Đây là một trong những thế mạnh của git là nhánh. Với git, việc quản lý nhánh rất dễ dàng. Mỗi nhánh trong Git gần giống như một workspace. Việc nhảy vào một nhánh để làm việc trong đó tương tự việc chuyển qua ngữ cảnh làm việc mới, và sau đó có thể nhanh chóng quay lại ngữ cảnh cũ.

Nhánh (branch) được dùng để phát triển tính năng mới mà không làm ảnh hưởng đến code hiện tại.

Nhánh master là nhánh “mặc định” khi bạn tạo một repository.
Nhánh master thông thường là nhánh chính của ứng dụng. Ví dụ bạn thử nghiệm một tính năng mới và muốn không ảnh hưởng đến code chính bạn có thể tạo một nhánh mới và sau khi xong sẽ hợp nhất lại với nhánh master. Việc hợp nhất 2 nhánh lại được gọi là merge.


#### d. Commit
Để ghi lại việc thêm/thay đổi file hay thư mục vào repository thì sẽ thực hiện thao tác gọi là Commit.

Khi thực hiện commit, trong repository sẽ tạo ra commit (hoặc revision) đã ghi lại sự khác biệt từ trạng thái đã commit lần trước với trạng thái hiện tại.

Commit này đang được chứa tại repository, các commit nối tiếp với nhau theo thứ tự thời gian. Bằng việc lần theo commit này từ trạng thái mới nhất thì có thể biết được lịch sử thay đổi trong quá khứ hoặc nội dung thay đổi đó.

![](https://2.bp.blogspot.com/-ck1jR2dDy6s/VTvIjBktgaI/AAAAAAAACVo/D-_6lpJqojQ/s1600/capture_intro1_3_1.png)

Các commit này, được đặt tên bởi 40 ký tự alphabet (mã md5 thì phải) không trùng nhau được băm từ thông tin commit. Bằng việc đặt tên cho commit, có thể chỉ định commit nào từ trong repository.

Mỗi commit đều có yêu cầu phải có commit message, để giải thích commit này là bạn đã làm gì trong này.
##### e. Các khái niệm khác
- Git Remote
- Working Tree và Index
- Trộn (Merge)
- Xung đột (Conflict)

### 3. Các GIT GUI client
- [SourceTree (Windows,Unix,MacOS)](https://www.sourcetreeapp.com/)
- [Tower (Windows, MacOS)](https://www.git-tower.com/)
- ....

### 2. Các câu lệnh thường dùng với GIT
##### a: Create a new local repository
- **git init**

##### b: Check out a repository
- Create a working copy of a local repository: **git clone /path/to/repository**
- For a remote server, use: **git clone username@host:/path/to/repository**

##### c: Add files
- Add one or more files to staging (index): **git add <filename>**
- Add one or more files to staging (index): **git add**

##### d: Commit
- Commit changes to head (but not yet to the remote repository): **git commit -m "Commit message"**
- Commit any files you've added with git add, and also commit any files you've changed since then: **git commit -a**

##### e: Push
- Send changes to the master branch of your remote repository:
**git push origin master**

##### f: Status
- List the files you've changed and those you still need to add or commit:	**git status**

Và còn rất nhiều lệnh khác, có thể tham khảo [đây](https://confluence.atlassian.com/bitbucketserver/basic-git-commands-776639767.html)
### 3. Quy trình làm việc với GIT
- Bước 1: Khởi tạo 1 repo

**git init**

hoặc clone 1 repo:

**git clone ssh://user@host/path/to/repo.git**
- Bước 2: Tạo thay đổi và xác nhận

**git status # View the state of the repo**

**git add <some-file> # Stage a file**

**git commit # Commit a file</some-file>**

- Bước 3: đẩy các xác nhận lên repo trung tâm

**git pull**
**git push origin master**
- Bước 4: quản lý Conflict


### 4. Các tài liệu nên tham khảo thêm
- Hướng dẫn về Git cơ bản cho người mới bắt đầu: Đọc ở [đây](https://backlog.com/git-tutorial/vn/intro/intro1_1.html) (Tiếng Việt), chú ý đọc cả phần Nhập môn và Phát triển.
- Sổ tay về Git: Đọc ở [đây](http://hnq90.github.io/git-guide/index.vi.html) hoặc [đây](https://learnxinyminutes.com/docs/vi-vn/git-vi/) (Tiếng Việt)
- Thực hành những thao tác căn bản với Git online: [Try Git](http://try.github.io/) (Tiếng Anh)
- Những lệnh hay dùng: [Git Cheatsheet](https://www.git-tower.com/blog/git-cheat-sheet/) (Tiếng Anh)
- Ebook hướng dẫn Git từ căn bản đến nâng cao: [Tiếng Anh](https://git-scm.com/book/en/v2) (updated 2014), [Tiếng Việt](https://git-scm.com/book/vi/v1) (updated 2009)
