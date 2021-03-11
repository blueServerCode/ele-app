<template>
    <div id="login">
        <img src="../assets/logo.jpg" alt="" />
        <!-- 手机号输入框 -->
        <InputGroup
            type="number"
            v-model="phone"
            placeholder="手机号"
            :btnTitle="btnTitle"
            :disabled="disabled"
            :error="errors.phone"
            @btnClick="getVerifyCode"
        />
        <!-- 验证码输入框 -->
        <InputGroup
            type="number"
            v-model="verifyCode"
            placeholder="验证码"
            :error="errors.code"
        />

        <!-- 用户协议 -->
        <div class="login_des">
            新用户登录即自动注册，表示已同意
            <span>《用户服务协议》</span>
        </div>
        <!-- 登录按钮 -->
        <div class="login_btn">
            <button :disabled="isClick" @click="handleLogin">登录</button>
        </div>
    </div>
</template>

<script>
import InputGroup from "../components/InputGroup";
export default {
    name: "",
    components: {
        InputGroup,
    },
    data() {
        return {
            phone: "",
            verifyCode: "",
            errors: {},
            btnTitle: "获取验证码",
            disabled: false,
        };
    },
    computed: {
        isClick() {
            if (this.phone && this.verifyCode) {
                return false;
            } else {
                return true;
            }
        },
    },
    methods: {
        handleLogin() {
            // 取消错误提醒
            this.errors = {};
            const data = {
                phone: this.phone,
                _id: '165184984'
            };
            localStorage.setItem("ele_login",JSON.stringify(data));
            this.$router.push("/");
        },
        getVerifyCode() {
            if (this.validatePhone()) {
                this.verifyCode = "123456";
                this.validateBtn();
            }
        },
        validateBtn() {
            let time = 60;
            let interval = setInterval(() => {
                if (time == 0) {
                    this.btnTitle = "获取验证码";
                    this.disabled = false;
                } else {
                    this.btnTitle = time + "秒后重试";
                    this.disabled = true;
                    time--;
                }
            }, 1000);
        },

        // 验证手机号是否能用，否则给error赋值，并且返回false
        validatePhone() {
            if (!this.phone) {
                this.errors = {
                    phone: "手机号码不能为空",
                };
                return false;
            } else if (!/^1[345678]\d{9}$/.test(this.phone)) {
                this.errors = {
                    phone: "请填写正确的手机号",
                };
                return false;
            } else {
                this.errors = {};
                return true;
            }
        },
    },
};
</script>

<style scoped>
#login {
    background-color: #ffffff;
    padding: 30px;
    box-sizing: border-box;
    text-align: center;
    width: 100%;
    height: 100%;
}
img {
    width: 150px;
}

.login_des {
    color: #aaa;
    line-height: 22px;
    margin-top: 10px;
}
.login_des span {
    color: #4d90fe;
}
.login_btn button {
    width: 100%;
    height: 40px;
    background-color: #48ca38;
    border-radius: 4px;
    color: white;
    font-size: 14px;
    border: none;
    outline: none;
    margin-top: 20px;
}
button[disabled] {
    background-color: #8bda8b;
}
</style>