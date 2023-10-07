<template>
    <div class="cron-com">
        <Tabs>
            <TabPane key="1" tab="秒">
                <Card class="card-top">
                    <RadioGroup
                        :value="radioValue['second']"
                        @change="
                            (e: any) => {
                                handleRadioChange(e, 'second');
                            }
                        "
                    >
                        <Radio :value="1">每秒执行</Radio>
                        <Radio :value="'period'">
                            周期从
                            <InputNumber
                                :disabled="radioValue['second'] !== 'period'"
                                :min="0"
                                :max="58"
                                :value="periodValue.second.min"
                                @change="(e: any) => handlePeriodChange(e as number, 'second', 'min')"
                            ></InputNumber>
                            -
                            <InputNumber
                                :disabled="radioValue['second'] !== 'period'"
                                :min="1"
                                :max="59"
                                :value="periodValue.second.max"
                                @change="(e: any) => handlePeriodChange(e as number, 'second', 'max')"
                            ></InputNumber>
                            秒
                        </Radio>
                        <Radio :value="'loop'">
                            从
                            <InputNumber
                                :disabled="radioValue['second'] !== 'loop'"
                                :min="0"
                                :max="58"
                                :value="loopValue.second.start"
                                @change="(e: any) => handleLoopChange(e as number, 'second', 'start')"
                            ></InputNumber>
                            秒开始，每
                            <InputNumber
                                :disabled="radioValue['second'] !== 'loop'"
                                :min="1"
                                :max="59"
                                :value="loopValue.second.end"
                                @change="(e: any) => handleLoopChange(e as number, 'second', 'end')"
                            ></InputNumber>
                            秒执行一次
                        </Radio>
                        <Row>
                            <Radio :value="'point'"> 指定 </Radio>
                            <Col>
                                <CheckboxGroup
                                    :disabled="radioValue['second'] !== 'point'"
                                    :value="pointValue.second"
                                    mode="multiple"
                                    :allow-clear="true"
                                    placeholder="请选择秒"
                                    @change="
                                        (value: any) =>
                                            handleCheckboxChange(
                                                value,
                                                'second',
                                                setPointValue
                                            )
                                    "
                                    :options="createSelectOption(59)"
                                >
                                </CheckboxGroup>
                            </Col>
                        </Row>
                    </RadioGroup>
                </Card>
            </TabPane>
            <TabPane key="2" tab="分">
                <Card class="card-top">
                    <RadioGroup
                        :value="radioValue.minute"
                        @change="(e: any) => handleRadioChange(e, 'minute')"
                    >
                        <Radio :value="1"> 每分执行 </Radio>
                        <Radio :value="'period'">
                            周期从
                            <InputNumber
                                :disabled="radioValue['minute'] !== 'period'"
                                :min="0"
                                :max="58"
                                :value="periodValue.minute.min"
                                @change="(e: any) => handlePeriodChange(e as number, 'minute', 'min')"
                            ></InputNumber>
                            -
                            <InputNumber
                                :disabled="radioValue['minute'] !== 'period'"
                                :min="1"
                                :max="59"
                                :value="periodValue.minute.max"
                                @change="(e: any) => handlePeriodChange(e as number, 'minute', 'max')"
                            ></InputNumber>
                            分
                        </Radio>
                        <Radio :value="'loop'">
                            从
                            <InputNumber
                                :disabled="radioValue['minute'] !== 'loop'"
                                :min="0"
                                :max="58"
                                :value="loopValue.minute.start"
                                @change="(e: any) => handleLoopChange(e as number, 'minute', 'start')"
                            ></InputNumber>
                            分开始，每
                            <InputNumber
                                :disabled="radioValue['minute'] !== 'loop'"
                                :min="1"
                                :max="59"
                                :value="loopValue.minute.end"
                                @change="(e: any) => handleLoopChange(e as number, 'minute', 'end')"
                            ></InputNumber>
                            分执行一次
                        </Radio>
                        <Row>
                            <Radio :value="'point'"> 指定 </Radio>
                            <Col>
                                <CheckboxGroup
                                    :disabled="radioValue['minute'] !== 'point'"
                                    :value="pointValue.minute"
                                    mode="multiple"
                                    :allow-clear="true"
                                    placeholder="请选择分"
                                    @change="
                                    (value: any) =>
                                        handleCheckboxChange(
                                            value,
                                            'minute',
                                            setPointValue
                                        )
                                "
                                    :options="createSelectOption(59)"
                                >
                                </CheckboxGroup>
                            </Col>
                        </Row>
                    </RadioGroup>
                </Card>
            </TabPane>
            <TabPane key="3" tab="时">
                <Card class="card-top">
                    <RadioGroup
                        :value="radioValue.hour"
                        @change="(e: any) => handleRadioChange(e, 'hour')"
                    >
                        <Radio :value="1"> 每时执行 </Radio>
                        <Radio :value="'period'">
                            周期从
                            <InputNumber
                                :disabled="radioValue['hour'] !== 'period'"
                                :min="0"
                                :max="22"
                                :value="periodValue.hour.min"
                                @change="(e: any) => handlePeriodChange(e as number, 'hour', 'min')"
                            ></InputNumber>
                            -
                            <InputNumber
                                :disabled="radioValue['hour'] !== 'period'"
                                :min="1"
                                :max="23"
                                :value="periodValue.hour.max"
                                @change="(e: any) => handlePeriodChange(e as number, 'hour', 'max')"
                            ></InputNumber>
                            时
                        </Radio>
                        <Radio :value="'loop'">
                            从
                            <InputNumber
                                :disabled="radioValue['hour'] !== 'loop'"
                                :min="0"
                                :max="22"
                                :value="loopValue.hour.start"
                                @change="(e: any) => handleLoopChange(e as number, 'hour', 'start')"
                            ></InputNumber>
                            时开始，每
                            <InputNumber
                                :disabled="radioValue['hour'] !== 'loop'"
                                :min="1"
                                :max="23"
                                :value="loopValue.hour.end"
                                @change="(e: any) => handleLoopChange(e as number, 'hour', 'end')"
                            ></InputNumber>
                            时执行一次
                        </Radio>
                        <Row>
                            <Radio :value="'point'"> 指定 </Radio>
                            <Col>
                                <CheckboxGroup
                                    :disabled="radioValue['hour'] !== 'point'"
                                    :value="pointValue.hour"
                                    mode="multiple"
                                    :allow-clear="true"
                                    placeholder="请选择时"
                                    @change="
                                    (value: any) =>
                                        handleCheckboxChange(
                                            value,
                                            'hour',
                                            setPointValue
                                        )
                                "
                                    :options="createSelectOption(23)"
                                >
                                </CheckboxGroup>
                            </Col>
                        </Row>
                    </RadioGroup>
                </Card>
            </TabPane>
            <TabPane key="4" tab="日">
                <Card class="card-top">
                    <RadioGroup
                        :value="radioValue.day"
                        @change="(e: any) => handleRadioChange(e, 'day')"
                    >
                        <Radio :value="1"> 每日执行 </Radio>
                        <Radio :value="2"> 不执行 </Radio>
                        <Radio :value="'period'">
                            周期从
                            <InputNumber
                                :disabled="radioValue['day'] !== 'period'"
                                :min="1"
                                :max="30"
                                :value="periodValue.day.min"
                                @change="(e: any) => handlePeriodChange(e as number, 'day', 'min')"
                            ></InputNumber>
                            -
                            <InputNumber
                                :disabled="radioValue['day'] !== 'period'"
                                :min="2"
                                :max="31"
                                :value="periodValue.day.max"
                                @change="(e: any) => handlePeriodChange(e as number, 'day', 'max')"
                            ></InputNumber>
                            日
                        </Radio>
                        <Radio :value="'loop'">
                            从
                            <InputNumber
                                :disabled="radioValue['day'] !== 'loop'"
                                :min="1"
                                :max="31"
                                :value="loopValue.day.start"
                                @change="(e: any) => handleLoopChange(e as number, 'day', 'start')"
                            ></InputNumber>
                            日开始，每
                            <InputNumber
                                :disabled="radioValue['day'] !== 'loop'"
                                :min="1"
                                :max="31"
                                :value="loopValue.day.end"
                                @change="(e: any) => handleLoopChange(e as number, 'day', 'end')"
                            ></InputNumber>
                            日执行一次
                        </Radio>
                        <Row>
                            <Radio :value="'point'"> 指定 </Radio>
                            <Col>
                                <CheckboxGroup
                                    :disabled="radioValue['day'] !== 'point'"
                                    :value="pointValue.day"
                                    mode="multiple"
                                    :allow-clear="true"
                                    placeholder="请选择日"
                                    @change="
                                    (value: any) =>
                                        handleCheckboxChange(
                                            value,
                                            'day',
                                            setPointValue
                                        )"
                                    :options="createSelectOption(31)"
                                >
                                </CheckboxGroup>
                            </Col>
                        </Row>
                    </RadioGroup>
                </Card>
            </TabPane>
            <TabPane key="5" tab="月">
                <Card class="card-top">
                    <RadioGroup
                        :value="radioValue.month"
                        @change="(e: any) => handleRadioChange(e, 'month')"
                    >
                        <Radio :value="1"> 每月执行 </Radio>
                        <Radio :value="2">不指定</Radio>
                        <Radio :value="'period'">
                            周期从
                            <InputNumber
                                :disabled="radioValue['month'] !== 'period'"
                                :min="1"
                                :max="11"
                                :value="periodValue.month.min"
                                @change="(e: any) => handlePeriodChange(e as number, 'month', 'min')"
                            ></InputNumber>
                            -
                            <InputNumber
                                :disabled="radioValue['month'] !== 'period'"
                                :min="2"
                                :max="12"
                                :value="periodValue.month.max"
                                @change="(e: any) => handlePeriodChange(e as number, 'month', 'max')"
                            ></InputNumber>
                            月
                        </Radio>
                        <Radio :value="'loop'">
                            从
                            <InputNumber
                                :disabled="radioValue['month'] !== 'loop'"
                                :min="1"
                                :max="12"
                                :value="loopValue.month.start"
                                @change="(e: any) => handleLoopChange(e as number, 'month', 'start')"
                            ></InputNumber>
                            月开始，每
                            <InputNumber
                                :disabled="radioValue['month'] !== 'loop'"
                                :min="1"
                                :max="12"
                                :value="loopValue.month.end"
                                @change="(e: any) => handleLoopChange(e as number, 'month', 'end')"
                            ></InputNumber>
                            月执行一次
                        </Radio>
                        <Row>
                            <Radio :value="'point'"> 指定 </Radio>
                            <Col>
                                <CheckboxGroup
                                    :disabled="radioValue['month'] !== 'point'"
                                    :value="pointValue.month"
                                    mode="multiple"
                                    :allow-clear="true"
                                    placeholder="请选择月"
                                    @change="
                                    (value: any) =>
                                        handleCheckboxChange(
                                            value,
                                            'month',
                                            setPointValue
                                        )
                                "
                                    :options="createSelectOption(12)"
                                >
                                </CheckboxGroup>
                            </Col>
                        </Row>
                    </RadioGroup>
                </Card>
            </TabPane>
            <TabPane key="6" tab="周">
                <Card class="card-top">
                    <RadioGroup
                        :value="radioValue.week"
                        @change="(e: any) => handleRadioChange(e, 'week')"
                    >
                        <Radio :value="1"> 每周执行 </Radio>
                        <Radio :value="2"> 不指定 </Radio>
                        <Row>
                            <Col>
                                <Radio :value="'period'"> 周期从 周 </Radio>
                            </Col>
                            <Col>
                                <Select
                                    :disabled="radioValue['week'] !== 'period'"
                                    :allow-clear="true"
                                    :value="periodValue.week.min"
                                    placeholder="请选择周"
                                    @change="(e: any) => handlePeriodChange(
                                    e as number, 'week', 'min'
                                )"
                                    :options="createWeekSelect(7)"
                                >
                                </Select>
                            </Col>
                            <Col>
                                <span> - 周 </span>
                            </Col>
                            <Col>
                                <Select
                                    :disabled="radioValue['week'] !== 'period'"
                                    :allow-clear="true"
                                    :value="periodValue.week.max"
                                    placeholder="请选择周"
                                    @change="(e: any) => handlePeriodChange(
                                    e as number, 'week', 'max'
                                )"
                                    :options="createWeekSelect(7)"
                                >
                                </Select>
                            </Col>
                        </Row>
                        <Row>
                            <Radio :value="'point'"> 指定 </Radio>
                            <Col>
                                <CheckboxGroup
                                    :disabled="radioValue['week'] !== 'point'"
                                    :value="pointValue.week"
                                    mode="multiple"
                                    :allow-clear="true"
                                    placeholder="请选择周"
                                    @change="
                                    (value: any) =>
                                        handleCheckboxChange(
                                            value,
                                            'week',
                                            setPointValue
                                        )
                                "
                                    :options="createWeekSelect(7)"
                                >
                                </CheckboxGroup>
                            </Col>
                        </Row>
                    </RadioGroup>
                </Card>
            </TabPane>
            <TabPane key="7" tab="年">
                <Card class="card-top">
                    <RadioGroup
                        :value="radioValue.year"
                        @change="(e: any) => handleRadioChange(e, 'year')"
                    >
                        <Radio :value="1"> 每年执行 </Radio>

                        <Radio :value="'period'">
                            周期从
                            <InputNumber
                                :disabled="radioValue['year'] !== 'period'"
                                :min="1970"
                                :max="2099"
                                :value="periodValue.year.min"
                                @change="(e: any) => handlePeriodChange(e as number, 'year', 'min')"
                            ></InputNumber>
                            -
                            <InputNumber
                                :disabled="radioValue['year'] !== 'period'"
                                :min="1971"
                                :max="2100"
                                :value="periodValue.year.max"
                                @change="(e: any) => handlePeriodChange(e as number, 'year', 'max')"
                            ></InputNumber>
                            年
                        </Radio>
                        <Radio :value="'loop'">
                            从
                            <InputNumber
                                :disabled="radioValue['year'] !== 'loop'"
                                :min="1970"
                                :max="2099"
                                :value="loopValue.year.start"
                                @change="(e: any) => handleLoopChange(e as number, 'year', 'start')"
                            ></InputNumber>
                            年开始，每
                            <InputNumber
                                :disabled="radioValue['year'] !== 'loop'"
                                :min="1"
                                :max="2100"
                                :value="loopValue.year.end"
                                @change="(e: any) => handleLoopChange(e as number, 'year', 'end')"
                            ></InputNumber>
                            年执行一次
                        </Radio>
                    </RadioGroup>
                </Card>
            </TabPane>
        </Tabs>
        <Card>
            <Row>
                <Col>时间表达式：</Col>
                <Col>
                    <Input placeholder="生成Cron" :value="cronText"></Input
                ></Col>
            </Row>
        </Card>
        <Card>
            <p>最近五次运行时间</p>
            <p v-for="item in resultTime" :key="item">{{ item }}</p>
        </Card>
    </div>
</template>
<script setup lang="ts" name="CronGenerator">
import { ref, watch } from "vue";
import { cronRunTime } from "./cronRuntime";
import {
    cronTimeEnum,
    IloopType,
    IperiodType,
    IpointType,
    IradioType,
} from "./cronTypes";
import {
    RadioChangeEvent,
    Tabs,
    TabPane,
    Card,
    RadioGroup,
    Radio,
    Input,
    InputNumber,
    Row,
    Col,
    Select,
    CheckboxGroup,
} from "ant-design-vue";
import { CheckboxValueType } from "ant-design-vue/lib/checkbox/interface";
const cronType = [
    "second",
    "minute",
    "hour",
    "day",
    "month",
    "week",
    "year",
] as cronTimeEnum[];

const props = defineProps<{
    cronExpression: string;
}>();

const emit = defineEmits<{
    (event: "expChange", value: string): void;
}>();

const cronText = ref("");
const editableCron = ref("");
// 单选
const radioValue = ref<IradioType>({
    second: 1,
    minute: 1,
    hour: 1,
    day: 1,
    month: 1,
    week: 1,
    year: 1,
});
const setPointValue = (val: IpointType) => {
    pointValue.value = val;
};
// 周期
const periodValue = ref<IperiodType>({
    second: { min: 1, max: 2 },
    minute: { min: 1, max: 2 },
    hour: { min: 0, max: 1 },
    day: { min: 1, max: 2 },
    month: { min: 1, max: 2 },
    week: { min: 2, max: 3 },
    year: { min: 2023, max: 2099 },
});
// 从...开始
const loopValue = ref<IloopType>({
    second: { start: 0, end: 1 },
    minute: { start: 0, end: 1 },
    hour: { start: 0, end: 1 },
    day: { start: 1, end: 1 },
    month: { start: 1, end: 1 },
    week: { start: 1, end: 1 },
    year: { start: 2023, end: 1 },
});
// 指定
const pointValue = ref<IpointType>({
    second: [],
    minute: [],
    hour: [],
    day: [],
    month: [],
    week: [],
    year: [],
});

// 最近运行时间
const resultTime = ref<string[]>([]);
watch(
    () => props.cronExpression,
    (val) => {
        if (val) {
            cronComeShow(val);
        } else {
            resetCronState();
        }
    }
);

watch(
    () => [radioValue.value, periodValue.value, loopValue.value],
    () => {
        createCron();
    }
);

watch(
    () => cronText.value,
    (val) => {
        emit("expChange", val);
    }
);

const getCron = () => {
    return cronText.value;
};

const getResultTime = () => {
    return resultTime.value;
};

const resetCronState = () => {
    cronType.forEach((item) => {
        radioValue.value[item] = 1;
        pointValue.value[item] = [];
    });
    periodValue.value = {
        second: { min: 1, max: 2 },
        minute: { min: 1, max: 2 },
        hour: { min: 0, max: 1 },
        day: { min: 1, max: 2 },
        month: { min: 1, max: 2 },
        week: { min: 2, max: 3 },
        year: { min: 2023, max: 2099 },
    };
    loopValue.value = {
        second: { start: 0, end: 1 },
        minute: { start: 0, end: 1 },
        hour: { start: 0, end: 1 },
        day: { start: 1, end: 1 },
        month: { start: 1, end: 1 },
        week: { start: 1, end: 1 },
        year: { start: 2023, end: 1 },
    };
    cronText.value = "";
};

const createCron = () => {
    let changeCron = {} as IradioType;
    cronType.forEach(
        (item) => (changeCron = { ...changeCron, ...cronGenerator(item) })
    );

    const { second, minute, hour, day, month, week, year } = changeCron;

    const tempText =
        second +
        " " +
        minute +
        " " +
        hour +
        " " +
        day +
        " " +
        month +
        " " +
        week +
        " " +
        year;
    cronText.value = tempText;
    resultTime.value = cronRunTime(tempText);
};

/**
 * cron生成器
 * @param type
 */
const cronGenerator = (type: cronTimeEnum) => {
    let srv = radioValue.value[type];
    let period = periodValue.value[type];
    let loop = loopValue.value[type];
    let param = pointValue.value[type];
    let data = "";
    switch (srv) {
        case 1:
            data = "*";
            break;
        case 2:
            data = "?";
            break;
        case "point":
            for (let v of param) {
                data = data + v + ",";
            }
            data = data.substring(0, data.length - 1);
            break;
        case "period":
            data = period.min + "-" + period.max;
            break;
        case "loop":
            data = loop.start + "/" + loop.end;
            break;
        default:
            data = "*";
    }

    return cronItemGenerator(type, data);
};

/**
 * 对象生成器
 * @param type
 * @param data
 * @returns {{second: *}|{minute: *}}
 */
const cronItemGenerator = (
    type: string,
    data: string
): { [key: string]: string } => {
    switch (type) {
        case "second":
            return { second: data };
        case "minute":
            return { minute: data };
        case "hour":
            return { hour: data };
        case "day":
            return { day: data };
        case "month":
            return { month: data };
        case "week":
            return { week: data };
        case "year":
            return { year: data };
        default:
            return {};
    }
};

/**
 * 生成 日期选择时间 options
 * @param num
 * @returns {lable:number,value:number}[]
 */
const createSelectOption = (
    num: number
): { label: number; value: number }[] => {
    let obj = [] as { label: number; value: number }[];
    for (let i = 0; i <= num; i++) {
        obj.push({
            label: i,
            value: i,
        });
    }
    return obj;
};

/**
 * 生成 week options
 * @param num
 * @returns {lable:string,value:number}[]
 */
const createWeekSelect = (num: number): { label: string; value: number }[] => {
    let obj = [] as { label: string; value: number }[];
    const weeks = ["", "一", "二", "三", "四", "五", "六", "日"];
    for (let i = 1; i <= num; i++) {
        obj.push({
            label: `星期${weeks[i]}`,
            value: i + 1 === 8 ? 1 : i + 1,
        });
    }
    return obj;
};

const cronValidator = (cronT: string) => {
    // 判断是否为正规的cron表达式
    const cronArr = cronT.split(" ");
    if (cronArr.length !== 6 && cronArr.length !== 7) {
        return false;
    }
    const cronReg = RegExp(
        "^\\s*($|#|\\w+\\s*=|(\\?|\\*|(?:[0-5]?\\d)(?:(?:-|\\/|\\,)(?:[0-5]?\\d))?(?:,(?:[0-5]?\\d)(?:(?:-|\\/|\\,)(?:[0-5]?\\d))?)*)\\s+(\\?|\\*|(?:[0-5]?\\d)(?:(?:-|\\/|\\,)(?:[0-5]?\\d))?(?:,(?:[0-5]?\\d)(?:(?:-|\\/|\\,)(?:[0-5]?\\d))?)*)\\s+(\\?|\\*|(?:[01]?\\d|2[0-3])(?:(?:-|\\/|\\,)(?:[01]?\\d|2[0-3]))?(?:,(?:[01]?\\d|2[0-3])(?:(?:-|\\/|\\,)(?:[01]?\\d|2[0-3]))?)*)\\s+(\\?|\\*|(?:0?[1-9]|[12]\\d|3[01])(?:(?:-|\\/|\\,)(?:0?[1-9]|[12]\\d|3[01]))?(?:,(?:0?[1-9]|[12]\\d|3[01])(?:(?:-|\\/|\\,)(?:0?[1-9]|[12]\\d|3[01]))?)*)\\s+(\\?|\\*|(?:[1-9]|1[012])(?:(?:-|\\/|\\,)(?:[1-9]|1[012]))?(?:L|W)?(?:,(?:[1-9]|1[012])(?:(?:-|\\/|\\,)(?:[1-9]|1[012]))?(?:L|W)?)*|\\?|\\*|(?:JAN|FEB|MAR|APR|MAY|JUN|JUL|AUG|SEP|OCT|NOV|DEC)(?:(?:-)(?:JAN|FEB|MAR|APR|MAY|JUN|JUL|AUG|SEP|OCT|NOV|DEC))?(?:,(?:JAN|FEB|MAR|APR|MAY|JUN|JUL|AUG|SEP|OCT|NOV|DEC)(?:(?:-)(?:JAN|FEB|MAR|APR|MAY|JUN|JUL|AUG|SEP|OCT|NOV|DEC))?)*)\\s+(\\?|\\*|(?:[0-6])(?:(?:-|\\/|\\,|#)(?:[0-6]))?(?:L)?(?:,(?:[0-6])(?:(?:-|\\/|\\,|#)(?:[0-6]))?(?:L)?)*|\\?|\\*|(?:MON|TUE|WED|THU|FRI|SAT|SUN)(?:(?:-)(?:MON|TUE|WED|THU|FRI|SAT|SUN))?(?:,(?:MON|TUE|WED|THU|FRI|SAT|SUN)(?:(?:-)(?:MON|TUE|WED|THU|FRI|SAT|SUN))?)*)(|\\s)+(\\?|\\*|(?:|\\d{4})(?:(?:-|\\/|\\,)(?:|\\d{4}))?(?:,(?:|\\d{4})(?:(?:-|\\/|\\,)(?:|\\d{4}))?)*))$"
    );
    if (!cronReg.test(cronT)) {
        return false;
    }
    return true;
};

/**
 * cron 回显
 * @param cronT
 */
const cronComeShow = (cronT: string) => {
    editableCron.value = cronT;
    if (!cronValidator(cronT)) {
        console.error("cron表达式不合法");
        return;
    }
    cronText.value = cronT;

    const cronArr = cronT.split(" ");
    const changeRadio = {} as IradioType;
    const initPeriodValue = {} as IperiodType;
    const initLoopValue = {} as IloopType;
    const initPointValue = {} as IpointType;

    cronArr.forEach((cron, index) => {
        if (cron.includes("*")) {
            changeRadio[cronType[index]] = 1;
        } else if (cron.includes("-")) {
            changeRadio[cronType[index]] = "period";
            initPeriodValue[cronType[index]] = {
                min: Number(cron.split("-")[0]),
                max: Number(cron.split("-")[1]),
            };
        } else if (cron.includes("/")) {
            changeRadio[cronType[index]] = "loop";
            initLoopValue[cronType[index]] = {
                start: Number(cron.split("/")[0]),
                end: Number(cron.split("/")[1]),
            };
        } else if (cron.includes("?")) {
            changeRadio[cronType[index]] = 2;
        } else {
            changeRadio[cronType[index]] = "point";
            initPointValue[cronType[index]] = cron
                .split(",")
                .map((item) => Number(item));
        }
    });

    periodValue.value = {
        ...periodValue.value,
        ...initPeriodValue,
    };
    loopValue.value = {
        ...loopValue.value,
        ...initLoopValue,
    };
    pointValue.value = {
        ...pointValue.value,
        ...initPointValue,
    };
    radioValue.value = {
        ...radioValue.value,
        ...changeRadio,
    };
    debugger;
};

/**
 * 单选按钮选择
 * @param e
 * @param type
 */
const handleRadioChange = (e: RadioChangeEvent, type: string) => {
    switch (type) {
        case "week":
            radioValue.value = {
                ...radioValue.value,
                day: 2,
                ...cronItemGenerator(type, e.target.value),
            };
            break;
        case "day":
            radioValue.value = {
                ...radioValue.value,
                week: 2,
                ...cronItemGenerator(type, e.target.value),
            };
            break;
        default:
            radioValue.value = {
                ...radioValue.value,
                ...cronItemGenerator(type, e.target.value),
            };
            break;
    }
};

/**
 * 指定时间选择
 * @param checkedValues
 * @param type
 * @param fun
 */
const handleCheckboxChange = (
    checkedValues: string | CheckboxValueType[],
    type: string,
    fun: Function
) => {
    fun({ ...pointValue.value, [type]: checkedValues });
    radioValue.value = {
        ...radioValue.value,
        [type]: "point",
    };
};

/**
 * 周期 InputNumber按钮选择
 * @param e
 * @param type
 * @param tar
 */
const handlePeriodChange = (e: number, type: cronTimeEnum, tar: string) => {
    const data = periodValue.value;
    data[type] =
        tar === "max"
            ? { max: e, min: data[type].min }
            : { max: data[type].max, min: e };
    periodValue.value = {
        ...periodValue.value,
        ...cronItemGenerator(type, data[type] as unknown as string),
    };
};

/**
 * 从...开始 InputNumber按钮选择
 * @param e
 * @param type
 * @param tar
 */
const handleLoopChange = (e: number, type: cronTimeEnum, tar: string) => {
    let data = loopValue.value;
    data[type] =
        tar == "start"
            ? { start: e, end: data[type].end }
            : { start: data[type].start, end: e };

    loopValue.value = {
        ...loopValue.value,
        ...cronItemGenerator(type, data[type] as unknown as string),
    };
};

defineExpose({
    getCron,
    getResultTime,
    resetCronState,
});
</script>

<style lang="scss" scoped></style>
