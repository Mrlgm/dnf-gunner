<template>
    <div>
        <el-select v-model="armorValue" clearable placeholder="请选择装备">
            <el-option
                    v-for="item in armor"
                    :key="item.id"
                    :label="item.name"
                    :value="item.id">
            </el-option>
        </el-select>
        <el-select v-model="armsValue" clearable placeholder="请选择武器">
            <el-option
                    v-for="item in arms"
                    :key="item.id"
                    :label="item.name"
                    :value="item.id">
            </el-option>
        </el-select>
        <el-select v-model="fashionValue" clearable placeholder="请选择时装">
            <el-option
                    v-for="item in fashion"
                    :key="item.id"
                    :label="item.name"
                    :value="item.id">
            </el-option>
        </el-select>
        <el-select v-model="haloValue" clearable placeholder="请选择光环">
            <el-option
                    v-for="item in halo"
                    :key="item.id"
                    :label="item.name"
                    :value="item.id">
            </el-option>
        </el-select>
        <el-select v-model="jewelryValue" clearable placeholder="请选择首饰">
            <el-option
                    v-for="item in jewelry"
                    :key="item.id"
                    :label="item.name"
                    :value="item.id">
            </el-option>
        </el-select>
        <el-select v-model="petValue" clearable placeholder="请选择宠物">
            <el-option
                    v-for="item in pet"
                    :key="item.id"
                    :label="item.name"
                    :value="item.id">
            </el-option>
        </el-select>
        <el-select v-model="privilegeValue" clearable placeholder="请选择特权">
            <el-option
                    v-for="item in privilege"
                    :key="item.id"
                    :label="item.name"
                    :value="item.id">
            </el-option>
        </el-select>
        <el-select v-model="specialEquipmentValue" clearable placeholder="请选择特殊装备">
            <el-option
                    v-for="item in specialEquipment"
                    :key="item.id"
                    :label="item.name"
                    :value="item.id">
            </el-option>
        </el-select>
        <el-select v-model="titleValue" clearable placeholder="请选择称号">
            <el-option
                    v-for="item in title"
                    :key="item.id"
                    :label="item.name"
                    :value="item.id">
            </el-option>
        </el-select>
        <el-select v-model="increaseLevelValue" clearable placeholder="请选择增幅水平">
            <el-option
                    v-for="item in increaseLevel"
                    :key="item.id"
                    :label="item.name"
                    :value="item.id">
            </el-option>
        </el-select>
        <el-select v-model="armorEnchantmentValue" clearable placeholder="请选择左侧附魔水平">
            <el-option
                    v-for="item in armorEnchantment"
                    :key="item.id"
                    :label="item.name"
                    :value="item.id">
            </el-option>
        </el-select>
        <el-select v-model="jewelryEnchantmentValue" clearable placeholder="请选择右侧附魔水平">
            <el-option
                    v-for="item in jewelryEnchantment"
                    :key="item.id"
                    :label="item.name"
                    :value="item.id">
            </el-option>
        </el-select>
        <el-input v-model="aa" placeholder="力量"></el-input>
        <el-input v-model="bb" placeholder="物攻"></el-input>
        <el-input v-model="cc" placeholder="属强"></el-input>
        <div>力量：{{powerAll}}</div>
        <div>力量百分比：{{poPowerAll}}</div>
        <div>攻击：{{atkAll}}</div>
        <div>攻击百分比：{{poAtkAll}}</div>
        <div>属强：{{strongAll}}</div>
        <div>黄字：{{huangAll}}</div>
        <div>白字：{{baiAll}}</div>
        <div>属性白：{{attBaiAll}}</div>
        <div>最终伤害：{{finalInjuryAll}}</div>
        <div>技能攻击力：{{skillAttackAll}}</div>
        <div>技能等级：{{skillLevelAll.sl15}}</div>
    </div>
</template>

<script>
    import armor from '../assets/armor'
    import arms from '../assets/arms'
    import fashion from '../assets/fashion'
    import halo from '../assets/halo'
    import jewelry from '../assets/jewelry'
    import pet from '../assets/pet'
    import privilege from '../assets/privilege'
    import specialEquipment from '../assets/specialEquipment'
    import title from '../assets/title'
    import increaseLevel from '../assets/increaseLevel'
    import armorEnchantment from '../assets/armorEnchantment'
    import jewelryEnchantment from '../assets/jewelryEnchantment'
    import {BigNumber} from 'bignumber.js';

    export default {
        name: "equipment",
        data() {
            return {
                aa: undefined,
                bb: undefined,
                cc: undefined,
                armor,
                armorValue: 9,
                arms,
                armsValue: 6,
                fashion,
                fashionValue: 2,
                halo,
                haloValue: 1,
                jewelry,
                jewelryValue: 6,
                pet,
                petValue: 6,
                privilege,
                privilegeValue: 0,
                specialEquipment,
                specialEquipmentValue: 3,
                title,
                titleValue: 10,
                increaseLevel,
                increaseLevelValue: 1,
                armorEnchantment,
                armorEnchantmentValue: 2,
                jewelryEnchantment,
                jewelryEnchantmentValue: 3
            }
        },
        computed: {
            form() {
                return [
                    this.armor[this.armorValue || 0],
                    this.arms[this.armsValue || 0],
                    this.fashion[this.fashionValue || 0],
                    this.halo[this.haloValue || 0],
                    this.jewelry[this.jewelryValue || 0],
                    this.pet[this.petValue || 0],
                    this.privilege[this.privilegeValue || 0],
                    this.specialEquipment[this.specialEquipmentValue || 0],
                    this.title[this.titleValue || 0],
                    this.armorEnchantment[this.armorEnchantmentValue || 0],
                    this.jewelryEnchantment[this.jewelryEnchantmentValue || 0]
                ]
            },
            powerAll() {
                let power = 1444
                this.form.forEach((obj) => {
                    power += obj.power
                })
                let aa = this.aa
                let zengfu = this.increaseLevel[this.increaseLevelValue || 0]
                power += zengfu.power
                power += parseInt(aa || 0)

                return power
            },
            poPowerAll() {
                let poPower = 0
                this.form.forEach((obj) => {
                    poPower += obj.poPower
                })
                return poPower
            },
            atkAll() {
                let atk = 105
                this.form.forEach((obj) => {
                    atk += obj.atk
                })
                let bb = this.bb
                atk += parseInt(bb || 0)
                return atk
            },
            poAtkAll() {
                let poAtk = 0
                this.form.forEach((obj) => {
                    poAtk += obj.poAtk
                })
                return poAtk
            },
            strongAll() {
                let strong = 33
                this.form.forEach((obj) => {
                    strong += obj.strong
                })
                let cc = this.cc
                strong += parseInt(cc || 0)
                return strong
            },
            huangAll() {
                let huang = 0
                this.form.forEach((obj) => {
                    huang += obj.huang
                })
                return huang
            },
            baiAll() {
                let bai = 0
                this.form.forEach((obj) => {
                    bai += obj.bai
                })
                return bai
            },
            attBaiAll() {
                let attBai = 0
                this.form.forEach((obj) => {
                    attBai += obj.attBai
                })
                return attBai
            },
            finalInjuryAll() {
                let finalInjury = 0
                this.form.forEach((obj) => {
                    finalInjury += obj.finalInjury
                })
                return finalInjury
            },
            skillAttackAll() {
                let skillAttack = 1
                this.form.forEach((obj) => {
                    let num = new BigNumber((obj.skillAttack + 100))
                    let pop = num.dividedBy(100)
                    skillAttack = parseFloat(pop.multipliedBy(skillAttack))
                })
                return skillAttack
            },
            skillLevelAll() {
                let skillLevel = {
                    sl15: 0,
                    sl20: 0,
                    sl25: 0,
                    sl30: 0,
                    sl35: 0,
                    sl40: 0,
                    sl45: 0,
                    sl48: 0,
                    sl50: 0,
                    sl70: 0,
                    sl75: 0,
                    sl80: 0,
                    sl85: 0
                }
                this.form.forEach((obj) => {
                    skillLevel.sl15 += obj.skillLevel15
                    skillLevel.sl20 += obj.skillLevel20
                    skillLevel.sl25 += obj.skillLevel25
                    skillLevel.sl30 += obj.skillLevel30
                    skillLevel.sl35 += obj.skillLevel35
                    skillLevel.sl40 += obj.skillLevel40
                    skillLevel.sl45 += obj.skillLevel45
                    skillLevel.sl48 += obj.skillLevel48
                    skillLevel.sl50 += obj.skillLevel50
                    skillLevel.sl70 += obj.skillLevel70
                    skillLevel.sl75 += obj.skillLevel75
                    skillLevel.sl80 += obj.skillLevel80
                    skillLevel.sl85 += obj.skillLevel85
                })
                return skillLevel
            }
        }
    }
</script>

<style lang="scss" scoped>

</style>