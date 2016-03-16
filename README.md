# Git 內部原理講解
Git 基本指令（本地端）
====================
- 操作環境：
 - OSX 10.10
 - Git 2.5.1

- 指令步驟

	1.驗證 git 檔案紀錄方式(sha-1 + 檔案內容)
	```shell
	echo 'test' >> test.md
	git add test.md
	tree . -a
	git hash-ject test.md
	echo 'test' | git hash-object --stdin
	```

	2.還原 sha-1 內容
	```shell
	find .git/objects -type f
	git cat-file -p 9daeafb9864cf43055ae93beb0afd6c7d144bfa4
	```

	3.認識 blob
	```
	git cat-file -t 9daeafb9864cf43055ae93beb0afd6c7d144bfa4
	```

	4.認識 commit
	```
	git commit -m 'Add test file'
	git cat-file -t 77f64af # commit
	git cat-file -p 77f64af # commit 內容
	git cat-file -t 9098a46b8a3cb674c82833688dfb5c77995053c2 # tree
	git cat-file -p 9098a46b8a3cb674c82833688dfb5c77995053c2 # 檔案類型, git 儲存類型, sha-1, 檔案名稱
	git cat-file -t 9daeafb9864cf43055ae93beb0afd6c7d144bfa4 # commit 內的檔案(blob)
	git cat-file -p 9daeafb9864cf43055ae93beb0afd6c7d144bfa4 # test
	```
