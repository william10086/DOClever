<template>
    <div style="width: 100%;">
        <table style="background-color: transparent;width: 100%;height: 100%">
            <thead>
            <th style="text-align: left;font-size: 20px">团队:</th>
            </thead>
            <tbody>
            <template v-for="n in arrLength">
                <tr>
                    <template v-for="index in 4">
                        <td  style="padding: 10px;height: 150px;width: 25%">
                            <div v-if="arr[(n-1)*4+(index-1)]" class="item" :style="{backgroundImage: 'url(\'../pic/back'+index+'.jpg\')',borderRadius:'5px',color:'gray',fontSize:'25px',display:'table'}" @click="info(arr[(n-1)*4+(index-1)])" @mouseenter="up($event)" @mouseleave="down($event)">
                                <div style="display: table-cell;vertical-align: middle">
                                    {{arr[(n-1)*4+(index-1)].name}}
                                </div>
                                <el-row class="row" style="height: 30px;line-height:30px;font-size: 15px;color: gray;position: absolute;left: 0;bottom: 0;text-align: left;background-color: rgba(215,215,215,0.51)">
                                    &nbsp;{{"成员:"+arr[(n-1)*4+(index-1)].userCount}}&nbsp;
                                    {{"项目:"+arr[(n-1)*4+(index-1)].projectCount}}
                                </el-row>
                            </div>
                        </td>
                    </template>
                </tr>
            </template>
            </tbody>
        </table>
    </div>
</template>
<style>
    .item{
        text-align: center;font-size:20px;color: #50a3ff;width: 100%;height: 100%;cursor: pointer;position: relative;box-shadow: 2px 2px 2px #888888;
    }
    @keyframes up {
        from {top:0px}
        to {top:-10px}
    }
    @keyframes down {
        from {top:-10px}
        to {top:0px}
    }
</style>
<script>
    module.exports={
        props:["arr"],
        data:function () {
            return {

            }
        },
        computed:{
            arrLength:function () {
                return Math.floor(this.arr.length/4)+1
            }
        },
        methods:{
            info:function (item) {
                session.set("teamId",item._id);
                session.set("teamName",item.name);
                session.set("teamRole",item.role);
                session.set("teamOwn",item.own);
                location.href="/html/web/team/team.html";
            },
            up:function (event) {
                event.target.style.animation="up 0.2s ease-out forwards"
            },
            down:function (event) {
                event.target.style.animation="down 0.2s ease-out forwards"
            }
        },
        events:{

        }
    }
</script>
