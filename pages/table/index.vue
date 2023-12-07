<template>
  <ClientOnly>
    <div
      content="此数据仅供企雀内部查看"
      class="flex flex-col flex-grow p-4">
      <section
        class="flex flex-row items-center justify-between pb-6">
        <a-card>
          <a-statistic
            title="今日提交反馈"
            :value="2"
            :value-style="{ color: '#3f8600' }"
            style="margin-right: 50px">
          </a-statistic>
          <a-statistic
            title="今日解决反馈"
            :value="2"
            :value-style="{ color: '#3f8600' }"
            style="margin-right: 50px">
          </a-statistic>
          <a-statistic
            title="今日复核反馈"
            :value="2"
            :value-style="{ color: '#3f8600' }"
            style="margin-right: 50px">
          </a-statistic>
        </a-card>
        <a-card>
          <a-statistic
            title="本周提交反馈"
            :value="2"
            :value-style="{ color: '#3f8600' }"
            style="margin-right: 50px">
          </a-statistic>
          <a-statistic
            title="本周解决反馈"
            :value="2"
            :value-style="{ color: '#3f8600' }"
            style="margin-right: 50px">
          </a-statistic>
          <a-statistic
            title="本周复核反馈"
            :value="2"
            :value-style="{ color: '#3f8600' }"
            style="margin-right: 50px">
          </a-statistic>
        </a-card>
        <a-card>
          <a-statistic
            title="当月提交反馈"
            :value="2"
            :value-style="{ color: '#3f8600' }"
            style="margin-right: 50px">
          </a-statistic>
          <a-statistic
            title="当月解决反馈"
            :value="2"
            :value-style="{ color: '#3f8600' }"
            style="margin-right: 50px">
          </a-statistic>
          <a-statistic
            title="当月复核反馈"
            :value="2"
            :value-style="{ color: '#3f8600' }"
            style="margin-right: 50px">
          </a-statistic>
        </a-card>
        <a-card>
          <a-statistic
            title="今年提交反馈"
            :value="2"
            :value-style="{ color: '#3f8600' }"
            style="margin-right: 50px">
          </a-statistic>
          <a-statistic
            title="今年解决反馈"
            :value="2"
            :value-style="{ color: '#3f8600' }"
            style="margin-right: 50px">
          </a-statistic>
          <a-statistic
            title="今年复核反馈"
            :value="2"
            :value-style="{ color: '#3f8600' }"
            style="margin-right: 50px">
          </a-statistic>
        </a-card>
        <a-card>
          <a-statistic
            title="累计提交反馈"
            :value="2"
            :value-style="{ color: '#3f8600' }"
            style="margin-right: 50px">
          </a-statistic>
          <a-statistic
            title="累计解决反馈"
            :value="2"
            :value-style="{ color: '#3f8600' }"
            style="margin-right: 50px">
          </a-statistic>
          <a-statistic
            title="累计复核反馈"
            :value="2"
            :value-style="{ color: '#3f8600' }"
            style="margin-right: 50px">
          </a-statistic>
        </a-card>
        <a-card>
          <a-statistic
            title="统计开始时间"
            :value="statisticsTotalDate"
            :value-style="{ color: '#3f8600' }"
            style="margin-right: 50px">
          </a-statistic>
          <a-statistic
            title="累计统计时间"
            :value="statisticsStartDate"
            :value-style="{ color: '#3f8600' }"
            style="margin-right: 50px">
          </a-statistic>
          <a-statistic
            title="系统提供"
            :value="'江俊鸿'"
            :value-style="{ color: '#3f8600' }"
            style="margin-right: 50px">
          </a-statistic>
        </a-card>
      </section>

      <a-form
        layout="inline"
        class="pb-6"
        :model="filterFrom">
        <a-form-item label="反馈项目">
          <a-select
            ref="select"
            v-model:value="filterFrom.questionProject"
            :options="questionProjectList"
            style="width: 120px">
          </a-select>
        </a-form-item>
        <a-form-item label="反馈类型">
          <a-select
            ref="select"
            v-model:value="filterFrom.questionType"
            :options="questionTypeList"
            style="width: 120px">
          </a-select>
        </a-form-item>
        <a-form-item label="反馈优先级">
          <a-select
            ref="select"
            v-model:value="filterFrom.questionPriority"
            :options="questionPriorityList"
            style="width: 120px">
          </a-select>
        </a-form-item>
        <a-form-item label="解决状态">
          <a-select
            ref="select"
            v-model:value="filterFrom.solveType"
            :options="solveTypeList"
            style="width: 120px">
          </a-select>
        </a-form-item>
        <a-form-item label="复核状态">
          <a-select
            ref="select"
            v-model:value="filterFrom.reCheckType"
            :options="reCheckTypeList"
            style="width: 120px">
          </a-select>
        </a-form-item>
        <a-form-item class="ml-auto">
          <a-button
            type="primary"
            @click="showModal"
            >提交反馈</a-button
          >
        </a-form-item>
      </a-form>

      <a-table
        :columns="columns"
        :data-source="data"
        bordered
        :pagination="paginationConfig"
        :scroll="{ x: 2000 }">
        <template #bodyCell="{ column, record }">
          <template
            v-if="
              column.key &&
              tagTypeColum.includes(column.key.toString())
            ">
            <a-tag
              class="text-sm py-1 px-2"
              color="volcano"
              :bordered="false">
              {{ record[column.key] }}
            </a-tag>
          </template>
          <template
            v-else-if="column.key === 'questionTime'">
            <span>{{ timeTest }}</span>
          </template>
          <template v-else-if="column.key === 'solveTime'">
            <span>{{ timeTest }}</span>
          </template>
          <template v-else-if="column.key === 'action'">
            <div class="flex flex-col items-center gap-y-4">
              <a-button type="primary">查看</a-button>
              <a-button
                type="primary"
                danger
                >删除</a-button
              >
            </div>
          </template>
        </template>
      </a-table>
    </div>

    <a-modal
      class="min-w-[80vw]"
      v-model:open="open"
      title="Basic Modal"
      @ok="handleOk">
      <a-form
        ref="formRef"
        name="custom-validation"
        :model="formState"
        :rules="rules"
        v-bind="layout"
        @finish="handleFinish"
        @validate="handleValidate"
        @finishFailed="handleFinishFailed">
        <a-form-item
          has-feedback
          label="Password"
          name="pass">
          <a-input
            v-model:value="formState.pass"
            type="password"
            autocomplete="off" />
        </a-form-item>
        <a-form-item
          has-feedback
          label="Confirm"
          name="checkPass">
          <a-input
            v-model:value="formState.checkPass"
            type="password"
            autocomplete="off" />
        </a-form-item>
        <a-form-item
          has-feedback
          label="Age"
          name="age">
          <a-input-number v-model:value="formState.age" />
        </a-form-item>
        <a-form-item :wrapper-col="{ span: 14, offset: 4 }">
          <a-button
            type="primary"
            html-type="submit"
            >Submit</a-button
          >
          <a-button
            style="margin-left: 10px"
            @click="resetForm"
            >Reset</a-button
          >
        </a-form-item>
      </a-form>
    </a-modal>
  </ClientOnly>
</template>
<script lang="ts" setup>
  import { useDateFormat, useNow } from '@vueuse/core';
  import type { Rule } from 'ant-design-vue/es/form';
  import type {
    FormInstance,
    SelectProps,
  } from 'ant-design-vue';

  useSeoMeta({
    title: '企雀问题反馈系统',
  });

  interface FormState {
    pass: string;
    checkPass: string;
    age: number | undefined;
  }

  const value1 = ref('全部');

  const filterFrom = ref({
    questionProject: '全部',
    questionType: '全部',
    questionPriority: '全部',
    solveType: '全部',
    reCheckType: '全部',
  });

  const statisticsTotalDate = useDateFormat(
    useNow(),
    'YYYY 年 MM 月 DD 号'
  ).value;

  const statisticsStartDate = useDateFormat(
    useNow(),
    'D 天 H 时 m 分 s 秒'
  ).value;

  const formRef = ref<FormInstance>();
  const formState = reactive<FormState>({
    pass: '',
    checkPass: '',
    age: undefined,
  });
  const checkAge = async (_rule: Rule, value: number) => {
    if (!value) {
      return Promise.reject('Please input the age');
    }
    if (!Number.isInteger(value)) {
      return Promise.reject('Please input digits');
    } else {
      if (value < 18) {
        return Promise.reject(
          'Age must be greater than 18'
        );
      } else {
        return Promise.resolve();
      }
    }
  };
  const validatePass = async (
    _rule: Rule,
    value: string
  ) => {
    if (value === '') {
      return Promise.reject('Please input the password');
    } else {
      if (formState.checkPass !== '') {
        formRef.value?.validateFields('checkPass');
      }
      return Promise.resolve();
    }
  };
  const validatePass2 = async (
    _rule: Rule,
    value: string
  ) => {
    if (value === '') {
      return Promise.reject(
        'Please input the password again'
      );
    } else if (value !== formState.pass) {
      return Promise.reject("Two inputs don't match!");
    } else {
      return Promise.resolve();
    }
  };

  const rules: Record<string, Rule[]> = {
    pass: [
      {
        required: true,
        validator: validatePass,
        trigger: 'change',
      },
    ],
    checkPass: [
      { validator: validatePass2, trigger: 'change' },
    ],
    age: [{ validator: checkAge, trigger: 'change' }],
  };
  const layout = {
    labelCol: { span: 4 },
    wrapperCol: { span: 14 },
  };
  const handleFinish = (values: FormState) => {
    console.log(values, formState);
  };
  const handleFinishFailed = (errors: any) => {
    console.log(errors);
  };
  const resetForm = () => {
    formRef.value?.resetFields();
  };
  const handleValidate = (...args: any) => {
    console.log(args);
  };

  const timeTest = useDateFormat(
    useNow(),
    'YYYY-MM-DD HH:mm:ss'
  ).value;

  const questionProjectList = ref<SelectProps['options']>([
    { value: '全部', label: '全部' },
    { value: '安卓App', label: '安卓App' },
    { value: '苹果App', label: '苹果App' },
    { value: '鸿蒙App', label: '鸿蒙App' },
    { value: '网页端', label: '网页端' },
    { value: 'Win客户端', label: 'Win客户端' },
    { value: 'Mac客户端', label: 'Mac客户端' },
  ]);

  const questionTypeList = ref<SelectProps['options']>([
    { value: '全部', label: '全部' },
    { value: 'Bug', label: 'Bug' },
    { value: '体验优化', label: '体验优化' },
    { value: '新需求', label: '新需求' },
  ]);

  const questionPriorityList = ref<SelectProps['options']>([
    { value: '全部', label: '全部' },
    { value: '一级', label: '一级' },
    { value: '二级', label: '二级' },
    { value: '三级', label: '三级' },
    { value: '四级', label: '四级' },
  ]);

  const solveTypeList = ref<SelectProps['options']>([
    { value: '全部', label: '全部' },
    { value: '待查看', label: '待查看' },
    { value: '已查看', label: '已查看' },
    { value: '解决中', label: '解决中' },
    { value: '已解决', label: '已解决' },
  ]);

  const reCheckTypeList = ref<SelectProps['options']>([
    { value: '全部', label: '全部' },
    { value: '待复核', label: '待复核' },
    { value: '复核中', label: '复核中' },
    { value: '已复核', label: '已复核' },
  ]);

  const columns = [
    {
      title: '反馈员工',
      dataIndex: 'questioner',
      key: 'questioner',
    },
    {
      title: '反馈项目',
      dataIndex: 'questionProject',
      key: 'questionProject',
    },
    {
      title: '反馈类型',
      dataIndex: 'questionType',
      key: 'questionType',
    },
    {
      title: '反馈优先级',
      dataIndex: 'questionPriority',
      key: 'questionPriority',
    },
    {
      title: '反馈描述',
      dataIndex: 'questionDesc',
      key: 'questionDesc',
    },
    {
      title: '反馈时间',
      key: 'questionTime',
      dataIndex: 'questionTime',
    },
    {
      title: '解决员工',
      dataIndex: 'solver',
      key: 'solver',
    },
    {
      title: '解决状态',
      dataIndex: 'solveType',
      key: 'solveType',
    },
    {
      title: '解决备注',
      dataIndex: 'solveDesc',
      key: 'solveDesc',
    },
    {
      title: '解决时间',
      dataIndex: 'solveTime',
      key: 'solveTime',
    },
    {
      title: '复核员工',
      dataIndex: 'reChecker',
      key: 'reChecker',
    },
    {
      title: '复核状态',
      dataIndex: 'reCheckType',
      key: 'reCheckType',
    },
    {
      title: '复核备注',
      dataIndex: 'reCheckDesc',
      key: 'reCheckDesc',
    },
    {
      title: '复核时间',
      dataIndex: 'reCheckTime',
      key: 'reCheckTime',
    },
    {
      title: '操作',
      key: 'action',
      dataIndex: 'action',
      fixed: 'right',
    },
  ];

  const tagTypeColum = [
    'questionProject',
    'questionType',
    'solveType',
    'questionPriority',
    'reCheckType',
  ];

  const data = [
    {
      questioner: '楚子航',
      questionProject: '安卓app',
      questionType: 'bug',
      questionDesc: '下拉框无法点击',
      questionPriority: '普通',
      questionTime: Math.floor(Date.now() / 1000),
      solver: '路明非',
      solveType: '已解决',
      solveDesc: 'bug已修复，请复测',
      solveTime: Math.floor(Date.now() / 1000),
      reChecker: '凯撒',
      reCheckType: '已解决',
      reCheckDesc: '已复核，bug已修复',
      reCheckTime: Math.floor(Date.now() / 1000),
    },
  ];

  const paginationConfig = {
    position: ['bottomCenter'],
  };

  const open = ref<boolean>(false);

  const showModal = () => {
    open.value = true;
  };

  const handleOk = (e: MouseEvent) => {
    console.log(e);
    open.value = false;
  };
</script>
