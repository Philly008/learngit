### Git���
����ʽ�汾����ϵͳ���汾���Ǽ��д��������������ġ�����Ҫ�������ܹ�����CVS��SVN���ǡ�  
�ֲ�ʽ�汾����ϵͳ��ÿ���˵ĵ����϶���һ�������İ汾�⡣��ȫ�Խϸߡ�Git���ǣ�������������������ǿ��ķ�֧����
### ��װGit
##### Linux�ϰ�װGit��
```shell
$ git       # �鿴 git�Ƿ�װ
$ sudo apt-get install git      # ��װ Git

$ tar -zxvf XXX.zip     # Դ�밲װ git
$ ./config
$ make
$ sudo make install
```
##### Mac �ϰ�װ Git��
ֱ�Ӵ� App Store��װ Xcode ��ѡ��˵���Xcode��>��Preferences��>"Downloads">"Command Line Tools">Install
##### Windows �ϰ�װ Git��
1.�ڹ���https://git-scm.com/downloads ���ز���װ��  
2.�˵��ҵ���Git������Git Bash����˵����װ�ɹ���  
3.���е�¼�ʺ��������ã�
```shell
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```
### �����汾�⣨repository��
**Windows�У�Ϊ�˱�����������Ī����������⣬��ȷ��Ŀ¼������������**
```shell
$ mkdir learngit
$ cd learngit
$ pwd
$ git init  # �ѵ�ǰĿ¼���Git���Թ���Ĳֿ�
$ ls -al    # ��ʾ����Ŀ¼�ļ�
```
���еİ汾����ϵͳ��ֻ�ܸ����ı��ļ��ĸĶ����޷�����ͼƬ����Ƶ��word�ȶ������ļ��ı仯��
```shell
# ���ļ���ӵ��汾��
$ git add readme.txt
$ git commit -m "wrote readme file"

$ git status    # �鿴�ֿ⵱ǰ��״̬
$ git diff readme.txt   # �鿴�޸ĵ�����
$ git log --pretty=oneline  # �鿴�ύ��ʷ��־
$ git reset --hard HEAD^    # HEAD ָ��ǰ�汾��HEAD^�ָ����ϸ��汾���ָ������ϸ��汾�� HEAD^^�������ۼ� ^
$ git reset --hard 1094a    # �ָ���ָ��ID������дID�Ĳ������ݣ���Ψһʶ�𼴿ɣ��汾
$ git reflog    # �鿴������ʷ
```
Git�������汾����ϵͳ��SVN��һ����֮ͬ���������ݴ����ĸ���  
��������Working Directory��:�������ܿ�����Ŀ¼����learngit ����һ����������  
�汾�⣨Repository������������һ������Ŀ¼ .git ��������㹤���������� Git�İ汾�⡣  
Git �İ汾����stage�����߽�index�����ݴ�������һ����֧master���Լ�ָ��master ��һ��ָ���HEAD��  
**git add����ʵ���Ͼ��ǰ�Ҫ�ύ�������޸ķŵ��ݴ�����stage����Ȼ��ִ�� git commit�Ϳ���һ���԰��ݴ����������޸��ύ����֧**  
git ��������޸ġ�
```shell
$ git diff HEAD -- readme.txt   # �鿴�������Ͱ汾���������°汾������
$ git checkout -- readme.txt    # �������������޸ģ��ð汾����İ汾�滻�������İ汾��
$ git reset HEAD readme.txt     # ���ݴ������޸ĳ�������unstage��
$ git rm test.txt   # �Ӱ汾����ɾ�����ļ�
```
### Զ�ֿ̲�
```shell
# 1. ���� SSH Key.���û���Ŀ¼�£�������û��.ssh Ŀ¼������У��ٿ������Ŀ¼����û�� id_rsa �� id_rsa.pub �������ļ�������Ѿ����ˣ�����ֱ��������һ�������û�У���Shell������ SSH Key��
$ ssh-keygen -t rsa -C "youremail@example.com"  # ������ .ssh Ŀ¼�� id_rsa��˽Կ�� �� id_rsa.pub����Կ�� �����ļ�
# 2. ��¼GitHub���򿪡�Account settings��>"SSH Keys">"Add SSH Key" ���������� Title����Key�ı�����ճ�� id_rsa.pub �ļ������ݡ�
$ git remote add origin git@github.com:Philly008/learngit.git   # ����һ��Զ�ֿ̲⣨Github���Ѵ���һ���ֿ� learngit��
$ git push -u origin master     # ��һ������master��֧���������ݡ���orgin��Git��Զ�̿�Ĭ�ϵĽз���
$ git clone git@github.com:Philly008/learngit.git  # ��Զ�ֿ̲��п�¡һ�����ؿ⡣
```
Git֧�ֶ���Э�飬����https����ͨ�� ssh ֧�ֵ�ԭ�� git Э���ٶ���졣
### ��֧����
```shell
$ git branch    # �鿴��֧
$ git branch dev    # ������֧ dev
$ git checkout dev  # �л���֧
$ git checkout -b dev   # ����+�л���֧��dev
$ git merge dev  # �ϲ�dev��֧����ǰ��֧
$ git branch -d dev     # ɾ����֧ dev
$ git merge feature1    # �ϲ������ֳ�ͻʱ�������ͻ����Git�ϲ�ʧ�ܵ��ļ��ֶ��༭Ϊ���������ݣ��������ύ
$ vim readme.txt    # �޸����ݣ�<<<<<<<��=======��>>>>>>>��ǳ���ͬ��֧������
$ git log --graph --pretty=online --abbrev-commit     # �鿴��֧�ϲ������
$ git merge --no-ff -m "merge with no-ff" dev   # ����Fast forward ģʽ��Git�ͻ���mergeʱ����һ���µ�commit���������ӷ�֧��ʷ�ϾͿ��Կ�����֧��Ϣ

$ git stash     # �ѵ�ǰ�����ֳ������ء����������Ժ�ָ��ֳ����������
$ git stash list     # �鿴����Ĺ����ֳ�
$ git stash pop     # �ָ���ͬʱ��stash����Ҳɾ��
$ git stash apply stash@{0}     # �ָ���ָ����stash

$ git branch -d feature-vulcan  # �޷�ɾ����֧ʱ
error: The branch 'feature-vulcan' is not fully merged.
If you are sure you want to delete it, run 'git branch -D feature-vulcan'.
$ git branch -D feature-vulcan  # ���� -D ����ǿ��ɾ��
```
### ����Э��
�����Զ�ֿ̲��¡ʱ��ʵ����Git�Զ��ѱ��ص�master��֧��Զ�̵�master��֧��Ӧ�����ˣ����ң�Զ�ֿ̲��Ĭ��������origin��
```shell
$ git remote    # �鿴Զ�̿����Ϣ
$ git remote -v # �鿴Զ�̿����ϸ��Ϣ
$ git push origin master    # �ѱ��ط�֧master���͵�Զ�̿�origin
$ git checkout -b dev origin/dev    # ����Զ��origin��dev��֧�����ط�֧dev

$ git push origin dev   # ����ʧ��ʱ��
$ git pull      # �����µ��ύ�� origin/devץ����������ͻ�����͡����������ʧ�ܣ�
$ git branch --set-upstream-to=origin/dev dev   # ���ñ���dev��Զ��origin/dev��֧�����ӣ��ٽ��� pull
```
**����Э���Ĺ���ģʽͨ����������**  
1. ���ȣ�������ͼ�� git push origin <branch-name> �����Լ����޸ģ�      
2. �������ʧ�ܣ�����ΪԶ�̷�֧����ı��ظ��£���Ҫ���� git pull ��ͼ�ϲ���
3. ����ϲ��г�ͻ��������ͻ�����ڱ����ύ��
4. û�г�ͻ���߽������ͻ������ git push origin <branch-name> ���;��ܳɹ���
5. ��� git pull ��ʾ no tracking information ����˵�����ط�֧��Զ�̷�֧�����ӹ�ϵû�д����������� git branch --set-upstream-to <branch-name> origin/<branch-name>
```shell
$ git log --graph --pretty=oneline --abbrev-commit
$ git rebase    # �ѷֲ���ύ��ʷ��������һ��ֱ�ߣ�����ȥ��ֱ��
```
### ��ǩ����
```shell
$ git branch    # �鿴���з�֧
$ git checkout master   # �л�����֧ master
$ git tag v1.0  # �ڵ�ǰ��֧�ϴ�һ���±�ǩ v1.0
$ git tag   # �鿴���б�ǩ
$ git log --pretty=oneline --abbrev-commit  # �鿴�ύ����ʷ
$ git tag v0.9 f52c622  # ��commit id Ϊ f52c622���ύ�����ǩ v0.9
$ git show v0.9     # �鿴��ǩ��Ϣ
$ git tag -a v0.1 -m "version 0.1 released" f52c622     # -a ָ����ǩ����-m ָ��˵������

$ git tag -d v0.1   # ɾ�����ر�ǩv0.1
$ git push origin v1.0  # ���ͱ�ǩv1.0��Զ��origin
$ git push origin --tags    # ��������δ���͵�Զ�̵ı��ر�ǩ
$ git tag -d v0.9   # ɾ��Զ�̱�ǩ����Ҫ��ɾ�����ر�ǩ
$ git push origin :refs/tags/v0.9   # �ٴ�Զ��ɾ��
```
**��ǩ���Ǻ�ĳ��commit�ҹ���������commit�ȳ�����master��֧���ֳ�����dev��֧����ô����������֧�϶����Կ��������ǩ**  
**ʹ��GitHub��**
1. ��GitHub�ϣ���������Fork��Դ�ֿ⣻
2. �Լ�ӵ��Fork��Ĳֿ�Ķ�дȨ�ޣ�
3. ��������pull request ���ٷ��ֿ������״��롣

```shell
$ git add -f App.class  # ǿ����ӵ�git 
$ git check-ignore -v App.class     # ��� .gitignore �ļ�����
$ git config --global alias.st status   # �������
$ git st    # ��ͬ�� git status
```
����ĳЩ�ļ�ʱ����Ҫ��д .gitignore;  
.gitignore �ļ�����Ҫ�ŵ��汾������ҿ��Զ� .gitignore ���汾����  
�����ļ���ԭ���ǣ�  
1. ���Բ���ϵͳ�Զ����ɵ��ļ�����������ͼ�ȣ�
2. ���Ա������ɵ��м��ļ�����ִ���ļ��ȣ�Ҳ�������һ���ļ���ͨ����һ���ļ��Զ����ɵģ����Զ����ɵ��ļ���û��Ҫ�Ž��汾�⣬����Java���������.class�ļ���
3. �������Լ��Ĵ���������Ϣ�������ļ��������ſ���������ļ���  
.gitignore �ļ����������ڣ�
```shell
# Windows:
Thumbs.db
ehthumbs.db
Desktop.ini

# Python:
*.py[cod]
*.so
*.egg
```












