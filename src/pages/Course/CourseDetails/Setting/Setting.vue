<template>
    <div class="base">
        <el-container>
            <!-- <el-header height="55px">
        <el-row>
          <div class="position">成员角色</div>
        </el-row>
      </el-header> -->
            <el-container>
                <el-main>
                    <el-tabs v-model="activeName" @tab-click="handleClick">
                        <el-tab-pane label="课程信息" name="课程信息">
                            <div>
                                <p>课程名称</p>
                                <el-input class='forinput' v-model="inputName" placeholder="请输入内容"></el-input>
                                <p>课程简介</p>
                                <el-input   type="textarea" class='forinput' v-model="inputDescription" placeholder="请输入内容"></el-input>
                                <el-button class='forbutton' type="primary" @click="">更新信息</el-button>
                            </div>
                        </el-tab-pane>
                        <el-tab-pane label="其他" name="其他">
                            <el-row>
                                <div class="more">
                                    <div class="project-more-content">
                                        <div style="text-align:left">
                                            <span style="font-size:18px;padding-left:5px">课程状态</span>
                                            <el-tag style="line-height: 19px;" size="mini" type="success">进行中</el-tag>
                                        </div >
                                        <p style="color: #909090;">更改当前项目状态</p>
                                    </div>
                                    <div class="project-more-action">
                                        <el-button size="small" type="primary" @click="" plain>完成项目</el-button>
                                    </div>
                                </div>
                            </el-row>
                            <el-row>
                                <div class="more">
                                    <div class="project-more-content">
                                        <div style="text-align:left">
                                            <span style="font-size:18px;padding-left:5px">删除课程</span>
                                            <!-- <el-tag style="line-height: 19px;" size="mini" type="success">进行中</el-tag> -->
                                        </div>
                                        <p style="color: #909090;">删除课程下所有资源</p>
                                    </div>
                                    <div class="project-more-action">
                                        <el-button type="danger" size="small" @click="" plain>删除课程</el-button>
                                    </div>
                                </div>
                            </el-row>
                        </el-tab-pane>
                    </el-tabs>
                </el-main>
            </el-container>
        </el-container>
    </div>
</template>
<script>
export default {
    data() {
        return {
            activeName: "课程信息",
            inputName: "",
            inputDescription: ""
        };
    },
    watch: {},
    created() {
        this.inputName=this.$route.params.courseId;
    },
    methods: {
        handleClick() {},
        // 加载失败的callback
        onErr(err) {
            console.log("pdf加载失败，请重试");
            console.log("错误信息：", err);
        }
    },
    components: {}
};
</script>
<style scoped>
.project-more-content {
    float: left;
}

.project-more-action {
    padding-top: 10px;
    vertical-align: middle;
    float: right;
}

.more {
    margin-top: 10px;
    /*width: 100%;*/
}

.forinput {
    padding-bottom: 10px;
}

.forbutton {
    margin-top: 5px;
    float: left;
}

p {
    float: left;
    font-size: 16px;
    margin-left: 5px;
    margin-bottom: 5px;
}

.base {
    box-shadow: 0 4px 6px 0 rgba(31, 31, 31, 0.05),
        0 0 2px 0 rgba(31, 31, 31, 0.2);
    /* margin: 10px; */
    /*min-width:1200px;*/
}

.el-row {
    background-color: white;
    border-bottom: 1px solid #dedede;
}

.position {
    /* min-height: 40px; */
    height: 44px;
    font-size: 25px;
    text-align: start;
    margin-top: 10px;
    margin-left: 15px;
}

.el-container {
    height: 100%;
    min-height: 1000px;
    padding-top: 0px;
}

.el-main {
    padding: 10px;
    background-color: white;
}

.el-header {
    padding: 0px;
}
</style>
