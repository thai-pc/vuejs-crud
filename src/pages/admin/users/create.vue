<template>
    <form @submit.prevent="createUsers()">
        <a-card title="Tạo mới tài khoản" style="width: 100%;">
            <div class="row mb-3">
                <div class="col-12 col-sm-4">
                    <div class="row">
                        <div class="col-12 d-flex justify-content-center mb-3">
                            <a-avatar shape="square" :size="200">
                                <template #icon><img src="../../../assets/users.jpg" alt="Avatar" /></template>
                            </a-avatar>
                        </div>
                        <div class="col-12 d-flex justify-content-center">
                            <a-button type="primary">
                                <font-awesome-icon :icon="['fas', 'plus']" class="me-2" />
                                <span>
                                    Chọn ảnh
                                </span>
                            </a-button>
                        </div>
                    </div>
                </div>
                <div class="col-12 col-sm-8">
                    <div class="row mb-3">
                        <div class="col-12 col-sm-3 text-start text-sm-end">
                            <label>
                                <span class="text-danger me-1">*</span>
                                <span :class="{ 'text-danger': errors.status_id }">Tình trạng:</span>
                            </label>
                        </div>
                        <div class="col-12 col-sm-5">
                            <a-select show-search placeholder="Tình trạng" style="width: 100%" :options="users_status"
                                :filter-option="filterOption" allow-clear v-model:value="users.status_id"
                                :class="{ 'select-danger': errors.status_id }"></a-select>
                            <div class="w-100"></div>
                            <small v-if="errors.status_id" class="text-danger">{{ errors.status_id[0] }}</small>
                        </div>
                    </div>
                    <div class="row mb-3">
                        <div class="col-12 col-sm-3 text-start text-sm-end">
                            <label>
                                <span class="text-danger me-1">*</span>
                                <span :class="{ 'text-danger': errors.username }">Tên tài khoản:</span>
                            </label>
                        </div>
                        <div class="col-12 col-sm-5">
                            <a-input placeholder="Tên tài khoản" allow-clear v-model:value="users.username"
                                :class="{ 'input-danger': errors.username }" />
                            <div class="w-100"></div>
                            <small v-if="errors.username" class="text-danger">{{ errors.username[0] }}</small>
                        </div>
                    </div>
                    <div class="row mb-3">
                        <div class="col-12 col-sm-3 text-start text-sm-end">
                            <label>
                                <span class="text-danger me-1">*</span>
                                <span :class="{ 'text-danger': errors.name }">Họ và tên:</span>
                            </label>
                        </div>
                        <div class="col-12 col-sm-5">
                            <a-input placeholder="Họ và tên" allow-clear v-model:value="users.name"
                                :class="{ 'input-danger': errors.name }" />
                            <div class="w-100"></div>
                            <small v-if="errors.name" class="text-danger">{{ errors.name[0] }}</small>
                        </div>
                    </div>
                    <div class="row mb-3">
                        <div class="col-12 col-sm-3 text-start text-sm-end">
                            <label>
                                <span class="text-danger me-1">*</span>
                                <span :class="{ 'text-danger': errors.name }">Email:</span>
                            </label>
                        </div>
                        <div class="col-12 col-sm-5">
                            <a-input placeholder="Email" allow-clear v-model:value="users.email"
                                :class="{ 'input-danger': errors.email }" />
                            <div class="w-100"></div>
                            <small v-if="errors.email" class="text-danger">{{ errors.email[0] }}</small>
                        </div>
                    </div>
                    <div class="row mb-3">
                        <div class="col-12 col-sm-3 text-start text-sm-end">
                            <label>
                                <span class="text-danger me-1">*</span>
                                <span :class="{ 'text-danger': errors.department_id }">Phòng ban:</span>
                            </label>
                        </div>
                        <div class="col-12 col-sm-5">
                            <a-select show-search placeholder="Phòng ban" style="width: 100%" :options="departments"
                                :filter-option="filterOption" allow-clear v-model:value="users.department_id"
                                :class="{ 'select-danger': errors.department_id }"></a-select>
                            <div class="w-100"></div>
                            <small v-if="errors.department_id" class="text-danger">{{ errors.department_id[0] }}</small>
                        </div>
                    </div>
                    <div class="row mb-3">
                        <div class="col-12 col-sm-3 text-start text-sm-end">
                            <label>
                                <span class="text-danger me-1">*</span>
                                <span :class="{ 'text-danger': errors.password }">Mật khẩu:</span>
                            </label>
                        </div>
                        <div class="col-12 col-sm-5">
                            <a-input-password placeholder="Mật khẩu" allow-clear v-model:value="users.password"
                                :class="{ 'input-danger': errors.password }" />
                            <div class="w-100"></div>
                            <small v-if="errors.password" class="text-danger">{{ errors.password[0] }}</small>
                        </div>
                    </div>
                    <div class="row mb-3">
                        <div class="col-12 col-sm-3 text-start text-sm-end">
                            <label>
                                <span class="text-danger me-1">*</span>
                                <span>Xác nhận mật khẩu:</span>
                            </label>
                        </div>
                        <div class="col-12 col-sm-5">
                            <a-input-password placeholder="Xác nhận mật khẩu" allow-clear
                                v-model:value="users.password_confirmation" />
                        </div>
                    </div>
                </div>
            </div>
            <div class="row">
                <div class="col-12 d-grid d-sm-flex justify-content-sm-end mx-auto">
                    <a-button class="me-0 me-sm-2 mb-sm-0 mb-3">
                        <router-link :to="{ name: 'admin-users' }">
                            <span>Hủy</span>
                        </router-link>
                    </a-button>
                    <a-button type="primary" html-type="submit">
                        <span>Lưu</span>
                    </a-button>
                </div>
            </div>
        </a-card>
    </form>
</template>
<script setup>
import { ref, reactive, toRefs } from 'vue';
import { useRouter } from 'vue-router';
import { message } from 'ant-design-vue';
import { useMenu } from '../../../stores/use-menu';
import axios from 'axios';

const store = useMenu();
store.onSelectedKeys(["admin-users"]);

const router = useRouter();
const users_status = ref([]);
const departments = ref([]);
const errors = ref({});
const users = reactive({
    username: '',
    name: '',
    email: '',
    password: '',
    password_confirmation: '',
    department_id: [],
    status_id: []
});

const filterOption = (input, option) => {
    return option.label.toLowerCase().indexOf(input.toLowerCase()) >= 0;
};

const getUsersCreate = () => {
    axios.get('http://127.0.0.1:8000/api/users/create')
        .then((response) => {
            const modifiedUsersStatus = response.data.users_status.map(item => ({
                value: item.id,
                label: item.name
            }));

            const modifiedDepartments = response.data.departments.map(item => ({
                value: item.id,
                label: item.name
            }));

            users_status.value = modifiedUsersStatus;
            departments.value = modifiedDepartments;
        })
        .catch((error) => {
            console.log(error);
        })
}
const createUsers = () => {
    axios.post('http://127.0.0.1:8000/api/users', users)
        .then((response) => {
            if (response.status == 200) {
                message.success('Tạo tài khoản thành công');
                router.push({ name: "admin-users" });
            }
        })
        .catch((error) => {
            errors.value = error.response.data.errors;
        })
}
() => ({
    ...toRefs(users)
})
getUsersCreate();


</script>

<style scoped>
.select-danger,
.input-danger {
    border: 1px solid red;
}
</style>