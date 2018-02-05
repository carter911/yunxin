# 网易云im
## 代码
~~~
<?php
namespace Common\Logic;
use yunxin\yunxin;


/**
 * YunxinLogic
 */
class YunxinLogic {

    protected $tableName = 'user';
    protected $yunxin = '';
    public function __construct()
    {
        parent::__construct();
        $AppKey         = '************';
        $AppSecret      = '****';
        $this->yunxin   = new yunxin($AppKey,$AppSecret,'curl');
    }

    /**
     * 创建用户
     * @param $accid
     * @param string $name
     * @param string $props
     * @param string $icon
     * @param string $token
     * @return array
     */
    public function createUser($accid, $name = '', $props = '', $icon = '', $token = '123456')
    {
        return $this->yunxin->createUserId($accid, $name, $props, $icon, $token);
    }


    /**
     * 创建群
     * @param $name
     * @param $create_id
     * @param array $users
     * @param string $description
     * @return array
     */
    public function createGroup($name, $create_id, $users = [], $description = '')
    {
        return $this->yunxin->createGroup($name, $create_id, $users, $description, '', 'invite', '0', '0','');
    }

    /**
     * 邀请人加入群聊
     * @param $group_id
     * @param $owner_id
     * @param array $users
     * @return array
     */
    public function addIntoGroup($group_id, $owner_id, $users=[])
    {
        return $this->yunxin->addIntoGroup($group_id, $owner_id, $users, '0', '施公宝邀请您加入群聊') ;
    }

    /**
     * 踢出群
     * @param $group_id
     * @param $owner_id
     * @param $member
     * @return array
     */
    public function kickFromGroup($group_id, $owner_id, $member)
    {
        return $this->yunxin->kickFromGroup($group_id, $owner_id, $member);
    }


    /**
     * 删除群
     * @param $group_id
     * @param $owner_id
     * @return array
     */
    public function removeGroup($group_id, $owner_id)
    {
        return $this->yunxin->removeGroup($group_id, $owner_id);
    }

    /**
     * 获取聊天记录
     * @param $group_id
     * @param $owner_id
     * @param string $start_time
     * @param string $end_time
     * @param int $limit
     * @param int $sort
     * @return array
     */
    public function historyGroup($group_id, $owner_id, $start_time = '', $end_time = '', $limit=100, $sort=2)
    {
        $start_time = empty($start_time)?time()*1000-2000000 : $start_time;
        $end_time = empty($end_time)?time()*1000 : $end_time;
        return $this->yunxin->queryGroupMsg($group_id, $owner_id, $start_time, $end_time, $limit, $sort );
    }


    public function test()
    {
        //群组功能（高级群）-创建群
        //print_r( $p->createGroup('groupname','chenrj',array('chenrj','chenrj001'),'','','invite','0','0','') );
        //群组功能（高级群）-拉人入群
        //print_r( $p->addIntoGroup('teamid','user1',array('user1','user2'),'0','请您入伙') );
        //群组功能（高级群）-踢人出群
        //print_r( $p->kickFromGroup('teamid','user1','user2' ) );
        //群组功能（高级群）-踢人出群
        //print_r( $p->removeGroup('teamid','user1' ) );
        //群组功能（高级群）-更新群资料
        //print_r( $p->updateGroup('teamid','user1','groupname') );
        //群组功能（高级群）-群信息与成员列表查询
        //print_r( $p->queryGroup(array('teamid1','teamid2') ) );
        //群组功能（高级群）-移交群主
        //print_r( $p->changeGroupOwner('teamid','user1','user1','2' ) );
        //群组功能（高级群）-任命管理员
        //print_r( $p->addGroupManager('teamid','user1',array('user2') ) );
        //群组功能（高级群）-移除管理员
        //print_r( $p->removeGroupManager('teamid','user1',array('user2') ) );
        //群组功能（高级群）-获取某用户所加入的群信息
        //print_r( $p->joinTeams('chenrj') );
        //群组功能（高级群）-修改群昵称
        //print_r( $p->updateGroupNick('teamid','user1','user1','xxx' ) );

        //历史记录-单聊
        //print_r( $p->querySessionMsg('user1','user2',(string)(time()*1000-2000000),(string)(time()*1000),'100','2' ) );
        //历史记录-群聊
        //print_r( $p->queryGroupMsg('teamid','user1',(string)(time()*1000-2000000),(string)(time()*1000),'100','2' ) );

        //发送短信验证码
        //print_r( $p->sendSmsCode('phonenum1','') );
        //校验验证码
        //print_r( $p->verifycode('phonenum1','验证码') );
        //发送模板短信
        //print_r( $p->sendSMSTemplate('templateid',array('phonenum1') ) );
        //查询模板短信发送状态
        //print_r( $p->querySMSStatus('templateid') );

        //发起单人专线电话
        // print_r( $p->startcall('Sulayman','13095088501','18085997799',90) );
        //发起专线会议电话
        //print_r( $p->startconf('user1','phonenum1',array('phonenum2','phonenum3'),60) );
        //查询单通专线电话或会议的详情
        //print_r( $p->queryCallsBySession('user1',sessionid) );

        //获取语音视频安全认证签名
        // print_r( $p->getUserSignature(1234) );

        //创建一个直播频道
        // print_r( $p->channelCreate('test_channel', 1) );
        //修改直播频道信息
        // print_r( $p->channelUpdate('test_channel', 'a918fdaf85a4458688e8f2789904ba6f', 1) );
        //删除一个直播频道
        // print_r( $p->channelDelete('a918fdaf85a4458688e8f2789904ba6f') );
        //获取一个直播频道的信息
        // print_r( $p->channelStats('a918fdaf85a4458688e8f2789904ba6f') );
        //获取用户直播频道列表
        // print_r( $p->channelList() );
        //重新获取推流地址
        // print_r( $p->channelRefreshAddr('a918fdaf85a4458688e8f2789904ba6f') );
    }
}
~~~
