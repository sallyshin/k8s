<template>
    <form @submit="onSubmit" class="item-form">
        <!-- 지역 -->
        <div class="form-control">
            <label>지역</label>
            <select name="region_cd" id="region_cd" v-model="region_cd" v-on:change="whenChangedRegion">
                <option :key="region.region_cd" v-for="region in regionCodes" :value="region.region_cd">{{ region.region_nm }}</option>
            </select>
        </div>
        <!-- 카테고리 -->
        <div class="form-control">
            <label>카테고리</label>
            <input type="text" name="cat_mst_cd" v-model="cat_mst_cd" placeholder="기본 카테고리">
            <input type="text" name="cat_dtl_cd" v-model="cat_dtl_cd" placeholder="상세 카테고리">
        </div>
        <!-- 품목명 -->
        <div class="form-control">
            <label>품목명</label>
            <input type="text" name="item_nm" v-model="item_nm" placeholder="품목명">
        </div>
        <!-- 제조사 -->
        <div class="form-control">
            <label>제조사명</label>
            <input type="text" name="company_nm" v-model="company_nm" placeholder="제조사명">
        </div>
        <!-- 수입국 -->
        <div class="form-control">
            <label>수입국</label>
            <input type="text" name="imported_from" v-model="imported_from" placeholder="수입국">
        </div>
        <!-- 수량 -->
        <div class="form-control">
            <label>수량</label>
            <input type="number" name="quantity" v-model="quantity" placeholder="수량">
        </div>
        <!-- 수입금지 여부 -->
        <div class="form-control form-control-check">
            <label>수입금지 여부</label>
            <input type="checkbox" name="is_banned" v-model="is_banned">
        </div>

        <!-- 저장하기 -->
        <input type="submit" value="저장" class="btn btn-block">
    </form>
</template>

<script>
export default {
    name: 'ItemForm',
    data() {
        return {
            // form 데이터
            nation_cd: '',
            item_cd: '',
            item_nm: '',
            region_cd: '',
            cat_mst_cd: '',
            cat_mst_nm: '',
            cat_dtl_cd: '',
            cat_dtl_nm: '',
            company_nm: '',
            imported_from: '',
            quantity: 0,
            is_banned: false,

            // 필요한 데이터들
            regionCodes: [
                { region_cd: '', region_nm: '전 지역' },
                { region_cd: 'ap-northeast-2', region_nm: '서울' },
                { region_cd: 'me-south-1', region_nm: '바레인' },
                { region_cd: 'us-east-1', region_nm: '켈리포니아' }
            ]
        }
    },
    created() {
        console.log("선택한 지역 >> [", this.region_cd, "]")
    },
    methods: {
        whenChangedRegion() {
            console.log("선택한 지역 >> [", this.region_cd, "]")
        },
        onSubmit(e) {
            e.preventDefault()
            if (!(this.region_cd && this.item_nm && this.cat_mst_cd && this.cat_dtl_cd && this.company_nm && this.imported_from && this.quantity && this.quantity > 0)) {
                alert("누락된 정보를 입력해주세요.")
                return
            }

            const newItem = {
                nation_cd: this.nation_cd,
                item_nm: this.item_nm,
                region_cd: this.region_cd,
                cat_mst_cd: this.cat_mst_cd,
                cat_dtl_cd: this.cat_dtl_cd,
                company_nm: this.company_nm,
                imported_from: this.imported_from,
                quantity: this.quantity,
                is_banned: this.is_banned
            }

            this.$emit('add-item', newItem)
        }
    },
    emits: ['add-item'],
}
</script>

<style scoped>
.item-form {
    margin-bottom: 40px;
}

.form-control {
    margin: 20px 0px;
}

.form-control label {
    display: block;
    font-weight: bold;
}

.form-control input {
    width: 100%;
    height: 40px;
    margin: 5px;
    padding: 3px 7px;
    font-size: 17px;
}

.form-control select {
    width: 50%;
    height: 40px;
    margin: 5px;
    padding: 3px 7px;
    font-size: 17px;
}

.form-control-check {
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.form-control-check label {
    flex: 1;
}

.form-control-check input {
    flex: 2;
    height: 20px;
}
</style>