<template>
  <div class="list-content">
    <template v-for="i of list">
      <h2 :id="i.title">{{ i.title }}</h2>
      <el-space
        wrap
        size="large"
        alignment="stretch"
      >
        <a
          v-for="j of i.children"
          :href="j.download[0].url"
          :target="j.download[0].url"
          rel="noopener noreferrer"
        >
          <el-card
            shadow="hover"
            class="box-card"
          >
            <template #header>
              <img
                :src="j.icon"
                :alt="'图标' + j.title"
              />
              <span> {{ j.title }}</span>
            </template>
            <div class="info">
              <p>
                {{ j.desc }}
              </p>
              <p v-for="k of j.download">
                <el-button
                  link
                  @click.prevent="open(k)"
                >
                  <span>
                    {{ k.name }}
                  </span>
                  <span v-if="k.code">&nbsp;&nbsp; 密码：{{ k.code }} </span>
                </el-button>
              </p>
            </div>
          </el-card>
        </a>
      </el-space>
    </template>
  </div>
</template>

<script setup lang="ts">
import list from "./software"

const open = (item: any) => {
  window.open(item.url)
}
</script>
<style lang="scss">
.software {
  h1 {
    display: none;
  }
  .container {
    max-width: unset !important;
    .content {
      max-width: unset !important;
      .content-container {
        max-width: unset !important;
      }
    }
  }
  .aside {
    position: fixed;
    right: 0;
    top: var(--vp-nav-height-desktop);
    z-index: 10;
    ul {
      list-style: none;
      margin: 0;
      padding: 0;
    }
  }
  .list-content {
    display: flex;
    flex-direction: column;
    align-content: center;
    justify-content: center;
    margin: auto;
    max-width: 1000px;
    padding: 32px 24px 96px;
    .box-card {
      width: 222px;
      height: 100%;
      .el-card__header {
        display: flex;
        align-items: center;
        span {
          padding-left: 1em;
        }
        img {
          width: 1.5em;
          height: 1.5em;
          border-radius: 4px;
        }
      }
      .info {
        p {
          color: var(--vp-c-black-mute);
        }
      }
    }
  }
}
</style>
