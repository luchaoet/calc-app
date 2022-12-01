<template>
	<div class="g-mw-1200 g-m-lr-a g-p-40">
		<p class="g-fs-28 g-m-b-20 g-ta-c g-fw-b g-lh-1">计算器</p>
		<el-form
			ref="ruleFormRef"
			:model="ruleForm"
			:rules="rules"
			label-width="120px"
			label-position="top"
		>
			<el-form-item label="Password" prop="pass">
				<el-input v-model="ruleForm.pass" autocomplete="off" clearable>
					<template #suffix>元</template>
				</el-input>
			</el-form-item>
			<el-form-item label="Confirm" prop="checkPass">
				<el-input
					v-model="ruleForm.checkPass"
					autocomplete="off"
					clearable
				>
					<template #suffix>元</template>
				</el-input>
			</el-form-item>
			<el-form-item label="Age" prop="age">
				<el-input v-model.number="ruleForm.age" clearable>
					<template #suffix>元</template>
				</el-input>
			</el-form-item>
			<el-form-item>
				<el-button type="primary" @click="submitForm(ruleFormRef)">计算</el-button>
				<el-button @click="resetForm(ruleFormRef)">重置</el-button>
			</el-form-item>
		</el-form>
	</div>
</template>

<script>
import { defineComponent, onMounted, reactive, ref, toRefs } from "vue";
// import Store from "electron-store";
// import { app, remote } from "electron";

export default defineComponent({
	name: "App",
	setup() {
		const ruleFormRef = ref();
		const state = reactive({
			ruleForm: {
				age: "",
				pass: "",
				checkPass: "",
			},
		});

		const rules = reactive({
			pass: [
				{
					required: true,
					message: "请输入xxx",
					trigger: "blur",
				},
			],
			checkPass: [
				{
					required: true,
					message: "请输入xxx",
					trigger: "blur",
				},
			],
			age: [
				{
					required: true,
					message: "请输入xxx",
					trigger: "blur",
				},
			],
		});

		const methods = reactive({
			submitForm: (formEl) => {
				if (!formEl) return;
				formEl.validate((valid) => {
					if (valid) {
						console.log(state.ruleForm);
					} else {
						console.log("error submit!");
						return false;
					}
				});
			},
			resetForm: (formEl) => {
				if (!formEl) return;
				formEl.resetFields();
			},
		});

		onMounted(() => {
			// const store = new Store();
			// store.set("foo", "bar");
			// // 根据process.type来分辨在哪种模式使用哪种模块
			// const APP = process.type === "renderer" ? remote.app : app;
			// // 获取electron应用的用户目录
			// const STORE_PATH = APP.getPath("userData");
			// console.log(STORE_PATH);
			// // 显示存储的信息
			// console.log(store.get("foo"));
		});

		return {
			rules,
			ruleFormRef,
			...toRefs(state),
			...toRefs(methods),
		};
	},
});
</script>

<style lang="scss">
.el-form-item:last-child {
	margin-bottom: 0;
}
</style>
