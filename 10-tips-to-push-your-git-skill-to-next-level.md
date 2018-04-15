# 10 mẹo để đẩy kỹ năng Git của bạn lên cấp độ tiếp theo

Gần đây chúng tôi đã xuất bản 2 bài hướng dẫn để cho bạn làm quen với Git cơ bản và sử dụng Git trong môi trường nhóm. Những lệnh mà chúng ta đã thảo luận  là về những gì đủ đề cho lập trình viên tồn tại trong thế giới Git. Trong bài viết này chúng ta sẽ thử khám phá làm thế nào để quản lý thời gian của bạn hiệu quả và tận dụng tính năng mà Git cung cấp.

Lưu ý: Một vài lệnh trong bài viết này bao gồm một phần của lệnh trong dấu ngoặc vuông. Ví dụ ( ```git add -p [file_name]``` ) . Trong những ví dụ đó, bạn sẽ cần thêm vào những số, định danh,…cần thiết không có ngoặc vuông.

## 1. Tự động hoàn thành lệnh Git

Nếu bạn chạy những lệnh thông qua CMD (command line), nó là nhiệm vụ mệt mỏi khi tự mình viết những lệnh. Để giúp điều đó, bạn có thể bật tính năng tự động hoàn thành lệnh của Git trong vài phút.

Để có được script này, chạy lệnh sau trên một hệ thống Unix:

```
cd ~
curl https://raw.github.com/git/git/master/contrib/completion/git-completion.bash -o ~/.git-completion.bash
```

Tiếp theo, thêm những dòng sau vào file ```~/.bash_profile```:

```
if [ -f ~/.git-completion.bash ]; then
    . ~/.git-completion.bash
fi
```

Mặc dù tôi đã đề cập trước đó, tôi không thể nhấn mạnh nó đủ rằng: nếu bạn muốn sử dụng những chức năng của Git đầy đủ, bạn chắc chắn nên chuyển sang giao diện dòng lệnh!

## 2. Bỏ qua tệp tin trong Git

Bạn có mệt mỏi với các tập tin biên dịch (kiểu như là ```.pyc```) tồn tại trong repository của Git? Hoặc là bạn quá chán mà đã up chúng vào Git? Nhìn đâu xa, có một cách mà thông qua đó bạn có thể nói với Git để bỏ qua hoàn toàn một số tập tin và thư mục. Đơn giản chỉ cần tạo một file có tên là ```.gitignore``` và liệt kê những tệp tin và thư mục mà không muốn Git theo dõi. Bạn có thể tạo ra ngoại lệ bằng cách sử dụng dấu chấm than (!).

```
*.pyc
*.exe
my_db_config/

!main.pyc
```

## 3. Ai đã làm xáo trộn code của tôi?

Nó là bản năng tự nhiên của con người đổ lỗi cho những người khác khi có một vài thứ sai. Nếu server sản phẩm của bạn bị lỗi, thật dễ dang để tìm ra thủ phạm - chỉ cần chạy ```git blame```. Nó là một lệnh cho bạn thấy tác giả của mọi dòng trong một tệp tin, commit đã cho thấy thay đổi cuối cùng trong dòng đó, và mốc thời gian của commit.

```
git blame [file_name]

```

![ahihi](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946443git-ninja-01.png)

Và trong ảnh chụp màn hình bên dưới, bạn có thể lệnh này trông thế nào trong một repository lớn hơn:

![ahihi](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946441git-ninja-02.png)

## 4. Lịch sử đánh giá của repository

Chúng ta đã một cái nhìn về việc sử dụng ```git log``` trong một hướng dẫn trước đó, tuy nhiên, đó là 3 lựa chọn mà bạn nên biết đến.

* ```--oneline``` – Phô bày thông tin hiển thị bên cạnh mỗi commit để giảm bớt commit lộn xộn và lời nhắn commit, tất cả hiển thị trong một dòng.
* ```--graph``` – Lựa chọn này vẽ một biểu diễn đồ họa dựa trên văn bản của lịch sử ở bên tay trái của output. Không sử dụng nếu bạn đang xem lịch sử của một nhánh đơn.
* ```--all``` – Hiển thị lịch sử của tất cả nhánh

Đây là việc kết hợp các tùy chọn sẽ trông giống như thế này: 

![ahihi](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946444git-ninja-03.png)

## 5. Đừng bao giờ quên theo dõi một commit

Hãy nói bạn đã commit một vài thứ nhưng bạn không muốn tiếp tục và thành ra bạn làm một reset cứng để quay lại trạng thái trước của bạn. Sau đó, bạn thấy bạn mất một vài thông tin khác trong tiến trình và muốn lấy lại nó, hoặc ít nhất là thấy nó. Đây là nơi có thể giúp ```git reflog```.

Một lệnh ```git log``` đơn giản cho bạn thấy lượt commit cuối cùng, tiền thân của nó, tiền thân của tiền thân của nó và vân vân.  Tuy nhiên, ```git reflog``` là một danh sách những commit mà phần đầu đã được chỉ đến. Nhớ rằng nó là nội bộ trong hệ thống của bạn; nó không phải là một phần của repository của bạn và không bao gồm trong push hoặc merge.
Nếu tôi chạy ```git log```, tôi có được những commit mà chúng là một phần của repository của tôi:

![ahihi](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946446git-ninja-04.png)

Tuy nhiên, lệnh ```git reflog``` cho bạn thấy một commit (```b1b0ee9 – HEAD@{4}```) đã bị mất khi tôi thực hiện một reset cứng:
![ahihi](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946447git-ninja-05.png)

## 6. Stage một phần của một file đã thay đổi cho một commit

Nó nói chung là một lần thực hành tốt để tạo những commit dựa trên tính năng, nghĩa la một commit phải dựa trên tính một tính năng hoặc một sửa lỗi. Hãy xem xét điều gì xảy ra khi bạn sửa hai lỗi, hoặc thêm nhiều những tính năng mà không commit những thay đổi đó. Trong một hoàn cảnh như vậy, bạn nên để những thay đổi trong một lần commit. Nhưng đây là một cách tốt hơn: Stage những file riêng biệt và commit chúng tách riêng nhau.

Giả sử bạn đã thực hiện nhiều thay đổi đến một file và muốn nó hiển thị trong những commit riêng biệt. Trong trường hợp này, chúng ta thêm những file đó bằng tiền tố ```-p``` vào những lệnh của chúng ta.

```

git add -p [file_name]

```

Cùng thử để chứng minh điều đó. Tôi đã thêm 3 dòng vào ```file_name``` và tôi chỉ muốn dòng đầu và dòng cuối hiển thị trong commit của tôi. Cùng nhìn lệnh ```git diff``` cho chúng ta xem.

![ahihi](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946449git-ninja-06.png)

Và cùng xem điều gì diễn ra khi chúng ta thêm ```-p``` vào lệnh ```add```

![ahihi](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946450git-ninja-07.png)

Có vẻ như Git cho rằng tất cả những thay đổi đều là một phần của cùng một ý tưởng, do đó nhóm nó thành một khối lớn. Bạn có các lựa chọn sau:

* Nhập y để stage khối đó
* Nhập n để không stage khối đó
* Nhập e để tự sửa khối đó
* Nhập d để thoát hoặc sang file khác
* Nhập s để tách khối đó

Trong trường hơp này, chúng ta chắc chắn muốn tách nó thành những phần nhỏ hơn để có thêm vài sự lựa chọn và bỏ qua phần còn lại.

![ahihi](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946452git-ninja-08.png)

Giống như bạn thấy, chúng ta đã thêm dòng đầu và dòng thứ 3 và bỏ qua dòng thứ 2. Bạn có thể xem trạng thái của repository và tạo một commit.

![ahihi](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946454git-ninja-09.png)

## 7. Nén nhiều commit

Khi bạn submit code của bạn cho việc xem xét và tạo một pull request ( nó xảy ra thường xuyên trong những dự án mở ), bạn đã có thể được yêu cầu để tạo một thay đổi cho code của bạn trước khi nó được chấp nhận. Bạn tạo sự thay đổi, chỉ để yêu cầu thay đổi nó lần nữa trong lần xem xét tiếp theo. Trước khi bạn biết nó, bạn có một vài lượt commit thêm. Theo ý tưởng, bạn có thể nén chúng vào trong một bằng việc sửa dụng lệnh ```rebase```.

```

git rebase -i HEAD~[number_of_commits]

```

Nếu bạn muốn nén 2 lần commit cuối, chạy lệnh sau.

```

git rebase -i HEAD~2

```

Với việc chạy lệnh này, bạn sẽ được đưa đến một giao diện tương tác liệt kê những lượt commit và yêu cầu bạn cái nào dùng để nén. Theo ý tưởng, bạn chạy ```pick``` vào commit cuối và chạy ```squash``` những cái cũ.

![ahihi](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946455git-ninja-10.png)

Sau đó bạn được yêu cầu để cung cấp một lời nhắn khi commit. Quá trình này cơ bản viết lại lịch sử những commit của bạn.

![ahihi](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946457git-ninja-11.png)

## 8. Giấu (stash) những commit chưa được thay đổi

Giả sử bạn đang làm việc trên một lỗi và một tính năng, bạn được yêu cầu trình diễn việc của bạn. Công việc hiện tại của bạn chưa đủ hoàn thành để được commit, và bạn không thể đưa ra một lần trình diễn trong giai đoạn này ( không  revert những thay đổi ). Trong hoàn cảnh này, lệnh ```git stash``` dùng để cứu nguy. Việc giấu diếm cơ bản là đưa tất cả những thay đổi và lưu trữ chúng cho lần sử dụng không xa. Để giấu (stash) thay đổi của bạn, đơn giản bạn chạy lệnh sau: 

```

git stash

```

Để kiểm tra danh sách bị giấu (stash), bạn có thể chạy:

```

git stash list

```

![ahihi](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946458git-ninja-12.png)

Nếu bạn muốn bỏ giấu (stash) và khôi phục những thay đổi chưa được commit, bạn áp dụng:

```

git stash apply

```

Trong ảnh chụp màn hình cuối, bạn có thể thấy mỗi lần giấu (stash) có một ID, một số duy nhất ( mặc dù chúng ta chỉ có một lần giấu (stash) trong trường hợp này ). Trong trường hợp bạn muốn áp dụng với những (stash) được chọn, bạn có thể thêm những ID rõ ràng vào lệnh ```apply```:

```

git stash apply stash@{2}

```

![ahihi](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946461git-ninja-13.png)


## 9. Kiểm tra commit bị mất

Mặc dù lệnh ```reflog``` là một cách để kiểm tra những commit bị mất, nó không tiện lợi trong những repository lớn. Đó là khi lệnh ```fsck``` ( viết tắt của file system check - kiểm tra tệp tin hệ thống) đi vào cuộc chơi.

```

git fsck --lost-found

```

![ahihi](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946463git-ninja-14.png)

Bạn có thể thấy commit bị mất ở đây. Bạn có thể kiểm tra những thay đổi trong commit bằng việc chạy lệnh ```git show [commit_hash]``` hoặc khôi phục nó bằng việc chạy lệnh```git merge [commit_hash]```.

```git fsck``` có sự thuận tiện hơn ```reflog```. Giả sửa bạn đã xóa một nhánh và sau đó clone repository. Với lệnh ```fsck```bạn có thể tìm kiếm và khôi phục nhánh bị xóa.


## 10. Hái anh đào ( lấp liếm )

Tôi đã lưu nhiều lệnh Git hay nhất cho người cuối cùng. Lệnh ```cherry-pick``` là lệnh Git yêu thích của tôi, bởi vì nghĩa đen cũng như tiện ích của nó vậy.

Trong cái đơn giản nhất của những điều khoản, ```cherry-pick``` đang chọn một commit từ một nhánh khác và hợp nhất nó với cái hiện tại. Nếu bạn đang làm việc một cách song song trên 2 hoặc nhiều nhánh, bạn có thể nhận biết một lỗi hiện tại trong tất cả các nhánh. Nếu bạn giải quyết nó trong một, bạn có thể lấp liếm commit trong những nhánh khác, không làm lộn xộn những tệp tin / commit khác.

Hãy xem xét một kịch bản nơi mà chúng ta có thể áp dụng điều đó. Tôi có 2 nhánh và tôi muốn dùng ```cherry-pick``` vào commit ```b20fd14: Cleaned junk``` trong một cái khác.

![ahihi](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946465git-ninja-15.png)

Tôi chuyển sang nhánh mà tôi muốn ```cherry-pick``` commit, chạy lệnh sau:

```

git cherry-pick [commit_hash]

```

![ahihi](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946467git-ninja-16.png)

Mặc dù chúng ta có một ```cherry-pick``` sạch trong lần này, bạn nên biết lệnh đó có thể thường xuyên dẫn đến xung đột (conflict), vì vậy dùng nó cẩn thận.

## Kết luận

Với điều này, chúng ta đến phần cuối của danh sách những mẹo mà tôi nghĩ có thể giúp kỹ năng dùng Git của bạn lên một cấp độ mới. Git là tốt nhất hiện có và nó có thể hoàn thành bất cứ điều gì bạn tưởng tượng. Vì vậy, thường xuyên thử thách thức bản thân với Git. Rất có thể, bạn sẽ kết thúc việc học một cái gì đó mới.
