<template>
    <div class="login_page" v-loading="loading">
        <transition name="form-fade" mode="in-out">
            <section class="form_contianer" v-show="showLogin">
                <div class="manage_tip">
                    <p>成绩管理系统</p>
                </div>
                <el-form :model="loginForm" :rules="rules" ref="loginForm">
                    <el-form-item prop="userName">
                        <el-input v-model="loginForm.userName" placeholder="用户名">
                            <span></span>
                        </el-input>
                    </el-form-item>
                    <el-form-item prop="password">
                        <el-input type="password" placeholder="密码" v-model="loginForm.passWord"></el-input>
                    </el-form-item>
                    <el-form-item>
                        <el-button type="primary" @click="submitForm('loginForm')" class="submit_btn">登陆</el-button>
                        <router-link :to="{name:'注册'}">
                            <p class="register">注册</p>
                        </router-link>
                    </el-form-item>
                </el-form>
            </section>
        </transition>
    </div>
</template>
<script>
import { mapActions, mapState, mapMutations } from "vuex";
import MYURL from "../../const/MYURL.js";
import { error } from "util";
export default {
    data() {
        return {
            loginForm: {
                userName: "",
                passWord: ""
            },
            rules: {
                userName: [
                    { required: true, message: "请输入用户名", trigger: "blur" }
                ],
                passWord: [
                    { required: true, message: "请输入密码", trigger: "blur" }
                ]
            },
            showLogin: false,
            loading: false
        };
    },
    mounted() {
        this.showLogin = true;
        let userInfo = JSON.parse(localStorage.getItem("userInfo"));
        console.log(userInfo);
    },
    computed: {
        ...mapState(["userInfo"])
    },
    methods: {
        ...mapActions(["LoginAction"]),
        submitForm(formName) {
            const UserName = this.loginForm.userName;
            this.$refs[formName].validate(valid => {
                if (valid) {
                    this.loading = true;
                    var data = {
                        teacherid: parseInt(this.loginForm.userName),
                        password: this.loginForm.passWord
                    };
                    this.$http
                        .post(
                            MYURL.Login,
                            JSON.stringify(data)
                            // {
                            //     headers:{
                            //         "Content-Type":"text/json;charset=UTF-8"
                            //     }
                            // }
                            // { emulateJSON: true }
                        )
                        .then(response => {
                            if (
                                response.status === 200 &&
                                response.body.code === 1
                            ) {
                                console.log(response.body);
                                console.log("验证通过");
                                let userInfo = {
                                    userName: UserName,
                                    userId: this.loginForm.userName
                                };
                                
                                //保存用户信息
                                this.LoginAction(userInfo);
                                console.log(
                                    "login.vue:" + JSON.stringify(this.userInfo)
                                );
                                localStorage.setItem(
                                    "userInfo",
                                    JSON.stringify(this.userInfo)
                                );

                                this.$message.success("登录成功");

                                this.$router.push({
                                    name: "Home",
                                    params: { teacherId: UserName }
                                });
                            } else {
                                this.$notify.error("用户名或密码错误");
                            }
                            this.loading = false;
                        })
                        .catch(error => {
                            // this.$router.push({
                            //     name: "Home",
                            //     params: { userName: UserName }
                            // });
                            this.$notify.error("服务器问题");
                            this.loading = false;
                        });
                } else {
                    // console.log('验证失败');
                    // this.loading = false

                    return false;
                }
            });
        }
    }
};
</script>
<style scoped>
.register {
    font-size: 10px;
    color: #909090;
}

.login_page {
    background-color: #324057;
    height: 100%;
}

.form_contianer {
    width: 400px;
    height: 320px;
    position: absolute;
    top: 50%;
    left: 50%;
    margin-left: -200px;
    margin-top: -160px;
    /*margin-top: 160px;
  margin-left: 105px;*/
    padding: 15px;
    border-radius: 5px;
    text-align: center;
    background-color: #fff;
}

.submit_btn {
    width: 40%;
    font-size: 16px;
}

.manage_tip {
    padding-bottom: 10%;
    width: 100%;
    top: 100px;
    left: 0;
}

.manage_tip p {
    font-size: 34px;
}

.tip {
    font-size: 12px;
    color: red;
}

.form-fade-enter-active,
.form-fade-leave-active {
    transition: all 1s;
}

.form-fade-enter,
.form-fade-leave-active {
    transform: translate3d(0, -50px, 0);
    opacity: 0;
}
</style>
