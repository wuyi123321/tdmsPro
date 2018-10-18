<template>
    <div class="sidebar">
        <el-menu class="sidebar-el-menu" :default-active="onRoutes" :collapse="collapse" background-color="#324157"
            text-color="#bfcbd9" active-text-color="#20a0ff" unique-opened router>
            <template v-for="item in items">
                <template v-if="item.subs">
                    <el-submenu :index="item.index" :key="item.index">
                        <template slot="title">
                            <i :class="item.icon"></i><span slot="title">{{ item.title }}</span>
                        </template>
                        <template v-for="subItem in item.subs">
                            <el-submenu v-if="subItem.subs" :index="subItem.index" :key="subItem.index">
                                <template slot="title">{{ subItem.title }}</template>
                                <el-menu-item v-for="(threeItem,i) in subItem.subs" :key="i" :index="threeItem.index">
                                    {{ threeItem.title }}
                                </el-menu-item>
                            </el-submenu>
                            <el-menu-item v-else :index="subItem.index" :key="subItem.index">
                                {{ subItem.title }}
                            </el-menu-item>
                        </template>
                    </el-submenu>
                </template>
                <template v-else>
                    <el-menu-item :index="item.index" :key="item.index">
                        <i :class="item.icon"></i><span slot="title">{{ item.title }}</span>
                    </el-menu-item>
                </template>
            </template>
        </el-menu>
    </div>
</template>

<script>
    import bus from '../common/bus';
    export default {
        data() {
            return {
                collapse: false,
                items: [
                    {
                        icon: 'el-icon-lx-people',
                        index: '1',
                        title: '用户权限',
                        subs: [
                            {
                                index: 'user_management',
                                title: '用户管理'
                            },
                            {
                                index: 'menu_management',
                                title: '角色权限'
                            }
                        ]
                    },
                    {
                        icon: 'el-icon-lx-apps',
                        index: '2',
                        title: '系统管理',
                        subs: [
                            {
                                index: 'projectPortfolioManagement',
                                title: '项目组管理'
                            },
                            {
                                index: 'sampleTypemManagement',
                                title: '样品类型管理'
                            },{
                                index: 'testStandardManagement',
                                title: '测试依据'
                            },{
                                index: 'testItemManagement',
                                title: '测试项目'
                            },{
                                index: 'testCategoryManagement',
                                title: '测试类别管理'
                            },{
                                index: 'sampleStorageManagement',
                                title: '样品储位管理'
                            },
                        ]
                    },
                    {
                        icon: 'el-icon-lx-apps',
                        index: '3',
                        title: '测试资源',
                        subs: [
                            {
                                index: 'laboratoryEquipmentCapability',
                                title: '实验室设备能力'
                            },
                            {
                                index: 'equipmentlLedger',
                                title: '设备台账'
                            },
                        ]
                    },
                    {
                        icon: 'el-icon-lx-apps',
                        index: '4',
                        title: '收样管理',
                        subs: [
                            {
                                index: 'confirmationoOfSample',
                                title: '样品确认'
                            },
                            {
                                index: 'sampleReceive',
                                title: '样品接收'
                            },{
                                index: 'sampleRent',
                                title: '样品领取'
                            },{
                                index: 'sampleReturn',
                                title: '样品归还'
                            }
                        ]
                    },{
                        icon: 'el-icon-lx-apps',
                        index: '5',
                        title: '排配系统',
                        subs: [
                            {
                                index: 'SampleFillet',
                                title: '样品排配'
                            },
                            {
                                index: 'channelInfo',
                                title: '通道信息'
                            }
                        ]
                    },{
                        icon: 'el-icon-lx-apps',
                        index: '6',
                        title: '测试任务',
                        subs: [
                            {
                                index: 'waitGetSamples',
                                title: '待领样'
                            },
                            {
                                index: 'waitTest',
                                title: '待测试'
                            }, {
                                index: 'testInProcess',
                                title: '测试中'
                            }
                        ]
                    },{
                        icon: 'el-icon-lx-apps',
                        index: '7',
                        title: '数据审核',
                        subs: [
                            {
                                index: 'dataAuditing',
                                title: '数据审核'
                            },
                            {
                                index: 'exceptionHandling',
                                title: '异常处理',
                                subs: [
                                    {
                                        index: 'SamplesAbnormal',
                                        title: '样品异常'
                                    },{
                                        index: 'testDataException',
                                        title: '测试数据异常'
                                    },{
                                        index: 'deviceExceptionHandling',
                                        title: '设备异常处理'
                                    },
                                ]
                            }
                        ]
                    },
                    {
                        icon: 'el-icon-lx-calendar',
                        index: '0',
                        title: '其他组件',
                        subs: [
                            {
                                index: 'form',
                                title: '基本表单'
                            },
                            {
                                icon: 'el-icon-lx-home',
                                index: 'dashboard',
                                title: '系统首页'
                            },
                            {
                                icon: 'el-icon-lx-cascades',
                                index: 'table',
                                title: '基础表格'
                            },
                            {
                                icon: 'el-icon-lx-copy',
                                index: 'tabs',
                                title: 'tab选项卡'
                            },
                            {
                                icon: 'el-icon-lx-emoji',
                                index: 'icon',
                                title: '自定义图标'
                            },
                            {
                                icon: 'el-icon-lx-favor',
                                index: 'charts',
                                title: 'schart图表'
                            },
                            {
                                icon: 'el-icon-rank',
                                index: 'drag',
                                title: '拖拽列表'
                            },
                            {
                                icon: 'el-icon-lx-warn',
                                index: '6',
                                title: '错误处理',
                                subs: [
                                    {
                                        index: 'permission',
                                        title: '权限测试'
                                    },
                                    {
                                        index: '404',
                                        title: '404页面'
                                    }
                                ]
                            },
                            {
                                index: '3-2',
                                title: '三级菜单',
                                subs: [
                                    {
                                        index: 'editor',
                                        title: '富文本编辑器'
                                    },
                                    {
                                        index: 'markdown',
                                        title: 'markdown编辑器'
                                    },
                                ]
                            },
                            {
                                index: 'upload',
                                title: '文件上传'
                            }
                        ]
                    },

                ]
            }
        },
        computed:{
            onRoutes(){
                return this.$route.path.replace('/','');
            }
        },
        created(){
            // 通过 Event Bus 进行组件间通信，来折叠侧边栏
            bus.$on('collapse', msg => {
                this.collapse = msg;
            })
        }
    }
</script>

<style scoped>
    .sidebar{
        display: block;
        position: absolute;
        left: 0;
        top: 70px;
        bottom:0;
        overflow-y: scroll;
    }
    .sidebar::-webkit-scrollbar{
        width: 0;
    }
    .sidebar-el-menu:not(.el-menu--collapse){
        width: 250px;
    }
    .sidebar > ul {
        height:100%;
    }
</style>
