<template>
    <el-dialog title="DOClever"  size="small" ref="box" :modal="hud">
        <el-row style="background-color: white;height: 100%;padding: 20px;" class="row">
            <el-input v-drag="'text'" type="textarea" :rows="6" :placeholder="placeholder" v-model="text"></el-input>
        </el-row>
        <el-row class="dialog-footer" slot="footer">
            <el-button type="primary" @click="save">
                保存
            </el-button>
        </el-row>
    </el-dialog>
</template>

<script>
    var dragFile=require("../director/dragFile")
    module.exports={
        props:["source","placeholder","hudremove"],
        data:function () {
            return {
                text:this.source,
                hud:this.hudremove===undefined?true:Boolean(this.hudremove)
            }
        },
        directives:{
            drag:dragFile
        },
        methods:{
            save:function () {
                this.$emit("save",this.text);
            }
        }
    }
</script>
