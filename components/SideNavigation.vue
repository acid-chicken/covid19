<template>
  <div class="SideNavigation">
    <div class="SideNavigation-HeadingContainer sp-flex">
      <v-icon
        class="SideNavigation-HeadingIcon pc-none"
        :aria-label="$t('Navi Open')"
        @click="openNavi"
      >
        mdi-menu
      </v-icon>
      <nuxt-link to="/" class="SideNavigation-HeadingLink">
        <div class="SideNavigation-Logo">
          <img src="/logo.png" :alt="$t('Nara')" />
        </div>
        <h1 class="SideNavigation-Heading">
          {{ $t('COVID-19') }}<br />{{ $t('Measures site') }}
        </h1>
      </nuxt-link>
    </div>
    <v-divider class="SideNavigation-HeadingDivider" />
    <div class="sp-none" :class="{ open: isNaviOpen }">
      <v-icon
        class="SideNavigation-ListContainerIcon pc-none"
        :aria-label="$t('Navi Close')"
        @click="closeNavi"
      >
        mdi-close
      </v-icon>
      <v-list :flat="true">
        <v-container
          v-for="(item, i) in items"
          :key="i"
          class="SideNavigation-ListItemContainer"
          @click="closeNavi"
        >
          <ListItem :link="item.link" :icon="item.icon" :title="item.title" />
          <v-divider v-show="item.divider" class="SideNavigation-Divider" />
        </v-container>
      </v-list>
      <div class="SideNavigation-Footer">
        <div class="SideNavigation-SocialLinkContainer">
          <a
            href="https://twitter.com/narakencyou"
            target="_blank"
            rel="noopener"
          >
            <img src="/twitter.png" alt="Twitter" />
          </a>
          <a
            href="https://www.facebook.com/office.pref.nara/"
            target="_blank"
            rel="noopener"
          >
            <img src="/facebook.png" alt="Facebook" />
          </a>
          <a
            href="https://line.me/R/ti/p/%40688bjyqz"
            target="_blank"
            rel="noopener"
          >
            <img src="/line.png" alt="Facebook" />
          </a>
          <a
            href="https://github.com/code4nara/covid19"
            target="_blank"
            rel="noopener"
          >
            <img src="/github.png" alt="GitHub" />
          </a>
        </div>
        <!-- <small class="SideNavigation-Copyright" lang="en">
          Copyright &copy; 2020 Tokyo Metropolitan Government. All Rights
          Reserved.
        </small> -->
      </div>
    </div>
  </div>
</template>

<i18n>
{
  "ja": {
    "Navi Open": "サイドメニュー項目を開く",
    "Navi Close": "サイドメニュー項目を閉じる",
    "Nara": "奈良県",
    "COVID-19": "新型コロナウイルス感染症",
    "Measures site": "まとめサイト（非公式）",
    "Nara Prefecture Government": "奈良県",
    "Tokyo COVID-19 Task Force": "新型コロナウイルス感染症対策本部",
    "The latest updates of NaraPref": "奈良県内の最新感染動向",
    "The latest updates of NaraCity": "奈良市内の最新感染動向",
    "For those concerned about novel coronavirus infections": "新型コロナウイルス感染症が心配なときに",
    "for Families with children": "お子様をお持ちの皆様へ",
    "school activity status": "各種学校の休校情報",
    "for Citizens": "県民の皆様へ",
    "for Enterprises and Employees": "中小企業・小規模事業者の皆様へ",
    "Official statements from Task Force": "奈良県総務部知事公室防災統括室",
    "Government official website": "奈良県公式ホームページ",
    "General Telephone Consultation": "一般電話窓口",
    "Departures and Contact Person Consultation Center": "新型コロナ・発熱患者受診相談窓口",
    "Board of Education Announcement": "教育委員会の発表",
    "Telephone consultation on labor-related matter": "労働関係の電話相談",
    "About us": "当サイトについて",
    "Municipalities": "奈良県内各市町村の関連ページ",
    "Other local Government": "他自治体の対策サイト"
  }
}
</i18n>

<script>
import ListItem from '@/components/ListItem'

export default {
  components: {
    ListItem
  },
  props: {
    isNaviOpen: {
      type: Boolean,
      required: true
    }
  },
  computed: {
    items() {
      return [
        {
          icon: 'mdi-chart-timeline-variant',
          title: this.$t('The latest updates of NaraPref'),
          link: '/',
          divider: true
        },
        {
          icon: 'covid',
          title: this.$t(
            'For those concerned about novel coronavirus infections'
          ),
          link:
            'http://www.pref.nara.jp/secure/226888/02_相談や受診の流れ0515.pdf'
        },
        {
          icon: 'mdi-account-multiple',
          title: this.$t('Departures and Contact Person Consultation Center'),
          link: 'http://www.pref.nara.jp/55410.htm#003'
        },
        {
          icon: 'mdi-account-multiple',
          title: this.$t('General Telephone Consultation'),
          link: 'http://www.pref.nara.jp/55410.htm#002',
          divider: true
        },
        {
          title: this.$t('Government official website'),
          link: 'http://www.pref.nara.jp/'
        },
        {
          title: this.$t('Municipalities'),
          link: '/municipalities',
          divider: true
        },
        {
          title: this.$t('for Enterprises and Employees'),
          link: 'http://www.pref.nara.jp/55408.htm'
        },
        {
          title: this.$t('Telephone consultation on labor-related matter'),
          link:
            'https://jsite.mhlw.go.jp/nara-roudoukyoku/content/contents/000611858.pdf'
        },
        {
          title: this.$t('Board of Education Announcement'),
          link: 'http://www.pref.nara.jp/kyoiku/'
        },
        {
          title: this.$t('school activity status'),
          link: 'https://crssrds.jp/school_info/',
          divider: true
        },
        {
          title: this.$t('About us'),
          link: '/about'
        },
        {
          title: this.$t('Other local Government'),
          link:
            'https://github.com/tokyo-metropolitan-gov/covid19/blob/development/FORKED_SITES.md'
        }
      ]
    },
    isClass() {
      return item => (item.title.charAt(0) === '【' ? 'kerningLeft' : '')
    }
  },
  methods: {
    openNavi() {
      this.$emit('openNavi')
    },
    closeNavi() {
      this.$emit('closeNavi')
    }
  }
}
</script>

<style lang="scss" scoped>
.SideNavigation {
  position: relative;
  height: 100%;
  background: $white;
  box-shadow: 0px 0px 2px rgba(0, 0, 0, 0.15);
  &-HeadingContainer {
    padding: 1.25em 0 1.25em 1.25em;
    align-items: center;
    @include lessThan($small) {
      padding: 7px 0 7px 20px;
    }
  }
  &-HeadingIcon {
    margin-right: 16px;
  }
  &-HeadingLink {
    @include lessThan($small) {
      display: flex;
      align-items: center;
    }
    text-decoration: none;
  }
  &-ListContainerIcon {
    margin: 24px 16px 0;
  }
  &-ListItemContainer {
    padding: 2px 20px;
  }
  &-Logo {
    margin: 20px 16px 0 0;
    width: 110px;
    @include lessThan($small) {
      margin-top: 0;
    }
  }
  &-Heading {
    margin-top: 8px;
    font-size: 13px;
    color: #898989;
    padding: 0.5em 0;
    text-decoration: none;
    @include lessThan($small) {
      margin-top: 0;
    }
  }
  &-HeadingDivider {
    margin: 0px 20px 4px;
    @include lessThan($small) {
      display: none;
    }
  }
  &-Divider {
    margin: 12px 0;
  }
  &-Footer {
    padding: 20px;
    background-color: $white;
  }
  &-SocialLinkContainer {
    display: flex;
    & img {
      width: 30px;
      &:first-of-type {
        margin-right: 10px;
      }
    }
  }
  &-Copyright {
    display: block;
    margin-top: 10px;
    font-size: 8px;
    line-height: 1.2;
    color: $gray-1;
    font-weight: bold;
  }
}
.open {
  @include lessThan($small) {
    position: fixed;
    overflow: auto;
    top: 0;
    bottom: 0;
    left: 0;
    display: block !important;
    width: 100%;
    z-index: z-index-of(opened-side-navigation);
    background-color: $white;
  }
}
@include largerThan($small) {
  .pc-none {
    display: none;
  }
}
@include lessThan($small) {
  .sp-flex {
    display: flex;
  }
  .sp-none {
    display: none;
  }
}
</style>
