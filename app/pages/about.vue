<template>
  <div class="container">
    <h1>안녕하세요!</h1>
    <p>이것은 대충 만든 내용입니다.</p>
    <div class="content-box">
      <h2>샘플 제목</h2>
      <p>여기에 대충 내용을 넣었습니다. 실제 프로젝트에서는 이 부분을 필요한 내용으로 교체하세요.</p>
      <ul>
        <li>항목 1</li>
        <li>항목 2</li>
        <li>항목 3</li>
      </ul>
    </div>
    <button class="btn">버튼</button>
  </div>
</template>

<script>
export default {
  name: 'SampleComponent',
  data() {
    return {
      message: '대충 만든 메시지'
    }
  }
}
</script>

<style scoped>
.container {
  padding: 20px;
  max-width: 800px;
  margin: 0 auto;
}
.content-box {
  border: 1px solid #ddd;
  padding: 15px;
  margin: 20px 0;
  border-radius: 5px;
}
.btn {
  background-color: #4CAF50;
  color: white;
  padding: 10px 15px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
</style>
