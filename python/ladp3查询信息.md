#ldap3查询用户信息
###环境: python3.5 + ldap3
<br/>
## **一. 查询用户信息**


	from ldap3 import Connection,Server,SUBTREE

	server = Server('ldap://192.168.3.22:389',get_info=None)

	class searchUser():
    conn = Connection(server, user='paicdom\liukai900', password='Lk031200')
    try:
        if conn.bind():
            print("连接ldap成功")
            baseDN = "dc=paicdom,dc=local"
            username = 'liukai900'
            searchFiltername = "sAMAccountName"
            searchFilter = '(' + searchFiltername + "=" + username + '*)'
            searchScope = SUBTREE
            searchList = ['name','telephoneNumber','memberOf','title','sn','department','mail','displayName','distinguishedName','company',
                          'sAMAccountName','manager','homePhone','mobile']
            result = conn.search(search_base=baseDN,search_filter=searchFilter,search_scope=searchScope,attributes=searchList)
            ldapInfoList = conn.response[0]
            print(conn.response)

    except Exception as e:
        print(e)
    finally:
        conn.unbind()

	searchUser()

## **二. 查询计算机信息**
    
	from ldap3 import Connection,Server,SUBTREE

	server = Server('ldap://192.168.3.22:389',get_info=None)

	class searchUser():
    conn = Connection(server, user='paicdom\liukai900', password='Lk031200')
    try:
        if conn.bind():
            print("连接ldap成功")
            baseDN = "dc=paicdom,dc=local"
            username = 'iqsz-l0001'
            searchFiltername = "sAMAccountName"
            searchFilter = '(' + searchFiltername + "=" + username + '$)'
            searchScope = SUBTREE
            result = conn.search(search_base=baseDN,search_filter=searchFilter,search_scope=searchScope,attributes=['*'])
            ldapInfoList = conn.response[0]
            print(conn.response)

    except Exception as e:
        print(e)
    finally:
        conn.unbind()

	searchUser()