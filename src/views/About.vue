<template>
  <div class="about">
    <el-main>
      <el-row type="flex" justify="center">
        <el-col :lg="20">
          <div class="grid-content bg-purple-dark">
            <div class="content">
              <img src="../../public/img/pagination.png" alt="pagination" />
              <div class="inner_content">
                <p>Инициализация компонента пагинации</p>
                <p>
                  <strong>prev-text</strong> - кнопка назад
                  <strong>next-text</strong> - кнопка вперёд
                </p>
                <p>
                  <strong>total</strong> - общее количество передаваемых елементов
                  <strong>page-size</strong> - количество елементов на странице
                </p>
                <p>
                  <strong>@current-change="Мой метод"</strong> - событие изменения страницы
                </p>
                <p>
                  <strong>:current-page="page"</strong> - текущая страница (выделяем активную страницу пагинации)
                </p>
              </div>
            </div>
          </div>

          <div class="grid-content bg-purple-dark">
            <div class="content">
              <img src="../../public/img/data.png" alt="data" />
              <div class="inner_content">
                <p>
                  <strong>elements: []</strong> - получаем с api все елементы етой модели
                </p>
                <p>
                  <strong>page: +this.$route.query.page || 1,</strong> - пагинация испольщует query params. Это нужно для того, чтобы если человек переходит по ссылке, то данные сохранялись
                </p>
                <p>
                  <strong>current_elements: [],</strong> - с помощтю библиотеки lodash мы разделяем массив elements на подмассивы. Сколько страниц столько и подмассивов
                </p>
              </div>
            </div>
          </div>

          <div class="grid-content bg-purple-dark">
            <div class="content">
              <img src="../../public/img/mounted.png" alt="mounted" />
              <div class="inner_content">
                <p>
                  С помощью библиотеки <strong>axios</strong> получаем данные по api
                </p>
                <p>
                  <strong>this.elements = res.data;</strong> присваиваем результат <strong>axios</strong> в модель elements
                </p>
                <p>
                  <strong>this.current_elements = _.chunk(res.data, this.elems_on_page);</strong> Делаем массив массивов (кол вложенных [] === кол страниц пагинации)
                </p>
                <p>
                  <strong>this.current_el = this.current_elements[this.page - 1] || this.current_elements[0];</strong> В зависимости от страницы выбираем подмассив. Страница 10 === this.current_elements[9]
                </p>
              </div>
            </div>
          </div>

          <div class="grid-content bg-purple-dark">
            <div class="content">
              <img src="../../public/img/change_page.png" alt="change_page" />
              <div class="inner_content">
                <p>
                  При изменении страницы срабатывает метод <strong> @current-change="mySuperChange"</strong>
                  Записываем в query params номер страницы и меняем текущий елемент массива
                </p>
              </div>
            </div>
          </div>

          <div class="grid-content bg-purple-dark">
            <div class="content">
              <img src="../../public/img/selectm.png" alt="change_page" />
              <div class="inner_content">
                <p>
                  Инициализируем select и навещиваем событие изменения
                </p>
                <p>
                  В зависимости от выбранного значения нужно пересчитать <strong>current_elements: []</strong> (новое количество страниц и елементов на странице. )
                  Превращаем в массив массивов по <strong>el</strong>  елементов в каждом
                </p>
                <p>меняем текущий выбранный елемент на новый</p>
              </div>
            </div>
          </div>

          <div class="grid-content bg-purple-dark">
            <div class="content">
              <img src="../../public/img/iteration.png" alt="iteration" />
              <div class="inner_content">
                <p>
                  Итерация массив происходит по <strong>current_el</strong> ЕТО ВАЖНО!
                </p>
              </div>
            </div>
          </div>

        </el-col>
      </el-row>
    </el-main>
  </div>
</template>

<style lang="scss">
.content {
  display: flex;
  justify-content: space-between;
  p{
    margin: 0.6rem 0
  }
  img{
    width: 49%;
  }
  .inner_content {
    width: 49%;
  }

}
.grid-content {
  padding: 1rem;
  background: aliceblue;
  margin-bottom: 1rem;
}
@media screen and (max-width: 568px) {
  .content{
    flex-direction: column;
    img{
      width: 100%;
      min-height: 170px;
    }
    .inner_content{
      width: 100%;
    }
  }
}
</style>