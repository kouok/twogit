# Git���ö��SSH-Key

�����ҵ�����Ҫ����git�˺ţ�һ����github�ģ�һ����gitee�ģ���ô����֮ǰ�Ƿ��ǰ�װ����һ��������Ҫ�������²�����У�

### ����

���ж��git�˺�ʱ�����磺

a. һ��gitee�����ڹ�˾�ڲ��Ĺ���������
b. һ��github�������Լ�����һЩ�������

### �������
1. ����һ����˾�õ�SSH-Key

`$ ssh-keygen -t rsa -C 'xxxxx@company.com' -f ~/.ssh/gitee_id_rsa`

2. ����һ��github�õ�SSH-Key

`$ ssh-keygen -t rsa -C 'xxxxx@qq.com' -f ~/.ssh/github_id_rsa`

�� ~/.ssh Ŀ¼���½�һ��config�ļ�������������ݣ�����Host��HostName��дgit��������������IdentityFileָ��˽Կ��·����
```
# gitee
Host gitee.com
HostName gitee.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/gitee_id_rsa
# github
Host github.com
HostName github.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/github_id_rsa
```

4. ��ssh����ֱ���ԣ������sshĿ¼�²��ԣ�

Ŀ¼һ��Ϊ`C:\Users\KOUOK\.ssh`

```
$ ssh -T git@gitee.com
$ ssh -T git@github.com
```
�ɹ��Ļ��᷵����������:

`Hi kouok! You've successfully authenticated, but GitHub does not provide shell access.`

5. ����û�гɹ������Ǳ����´���������Ϊû����github��gitee�����ssh keys

`Permission denied (publickey).` 

6. ����Ҫ��github��gitee�����������ssh  keys

github����ӣ��ҵ�`github_id_rsa.pub`�򿪣�������������д��뵽github��ssh keys��

gitee����ӣ��ҵ�`gitee_id_rsa.pub`�򿪣�������������д��뵽gitee��ssh keys��

Ȼ���ٲ��ԣ�

### ��ηֱ��ύ����ͬ��Զ�̷������У�ָ���ύ��github����gitee��

1. ����1-���ϵ����£��Ѿ�������clone�������£���ô���Ѿ������������Ͻ����˹�������ʱ����ֱ����ƽ�������ύ
2. ����2-���µ����ϣ�Ҳ�����ڱ��ش����ļ��У�Ȼ�������ļ������͵�������������ͬgithub֮ǰ�ģ����£�

```
a���ڱ����½�һ���ļ��У�����Ϊ��Ŀ���֣�ע�⣺��Ҫ��Ŀ��Ƕ����Ŀ��
b��`git init` ��ʼ�������ļ���Ϊһ��github��Ŀ��
c��`git add .` ����
d��`git commit -m "ע��"`  �ύ���ݴ���
e�����������ǽ����ص������ϵĿ���й��������Ե�����ȥ�½�һ��һģһ�����ֵ�Զ�̿�
f��`git remote add origin Զ�̿��ַ`������`git remote add origin https://github.com/kouok/web14-gitbash.git`
�����ص������ϵĽ��й���
g��`git push -u origin master`  �����µ�ͬ��������ȥ��
f���������ɾ�Ĳ�Ȳ���ȫ�������һ������һ���ˡ�
```