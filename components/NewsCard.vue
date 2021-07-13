<template>
  <div class="mx-5">
    <div class="container">
      <h2 class="text-center mr-3">News App using Nuxt</h2>
      <div>
        <b-form @submit="handleClick()">
          <div>
            <b-form-input
              v-model="search"
              placeholder="please search here"
            ></b-form-input>
          </div>
          <div class="text-center my-3">
            <b-button squared variant="success" @click="handleClick"
              >Search</b-button
            >
          </div>
        </b-form>
      </div>
      <div>
        <div v-if="loading" class="text-center py-2">
          <div class="spinner-border text-primary" role="status">
            <span class="sr-only">Loading...</span>
          </div>
          Getting news
        </div>
        <b-row v-if="!loading">
          <b-col
            v-for="(news, index) in newsCart"
            :key="index"
            cols="12"
            md="6"
            lg="3"
          >
            <b-card-group>
              <b-card
                :img-src="news.urlToImage"
                img-width="150px"
                img-height="200px"
                img-alt="Image"
                img-top
                class="my-2"
              >
                <b-card-text>
                  {{ news.description }}
                </b-card-text>

                <a :href="news.url" target="_blank"
                  ><b-button block variant="success">Read more</b-button></a
                >
              </b-card>
            </b-card-group>
          </b-col>
        </b-row>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'NewsCard',
  data() {
    return {
      search: '',
      url: 'https://newsapi.org/v2/everything',
      country: '',
      newsCart: [
        {
          source: {
            id: 'mashable',
            name: 'Mashable',
          },
          author: 'Stan Schroeder',
          title:
            'Elon Musk says Tesla will resume Bitcoin purchases when Bitcoin gets greener',
          description:
            "It's all about clean energy, it seems. \nElon Musk and Tesla caused ripples in the cryptocurrency market in the past few months, first by announcing that Tesla had bought $1.5 billion worth of bitcoins and that it will start accepting Bitcoin for purchases, an…",
          url: 'https://mashable.com/article/tesla-bitcoin-purchases-green/',
          urlToImage:
            'https://mondrian.mashable.com/2021%252F06%252F14%252Fcc%252Faf6b974e89a64972a334f8675f5dc80a.36e5a.jpg%252F1200x630.jpg?signature=XiWTfhyod6_Xl2i4nyhER_1xCXQ=',
          publishedAt: '2021-06-14T07:15:49Z',
          content:
            "It's all about clean energy, it seems. \r\nElon Musk and Tesla caused ripples in the cryptocurrency market in the past few months, first by announcing that Tesla had bought $1.5 billion worth of bitcoi… [+2508 chars]",
        },
        {
          source: {
            id: 'the-verge',
            name: 'The Verge',
          },
          author: 'Richard Lawler',
          title:
            'Kaseya ransomware attackers demand $70 million, claim they infected over a million devices',
          description:
            'Three days after ransomware attackers hijacked a managed services platform, recovery efforts continued. The REvil group is reportedly asking for as much as $70 million in Bitcoin to unlock the more than 1 million devices infected.',
          url: 'https://www.theverge.com/2021/7/5/22564054/ransomware-revil-kaseya-coop',
          urlToImage:
            'https://cdn.vox-cdn.com/thumbor/nk-drxT0WYuHTTAQw6MhPgi4LK8=/0x146:2040x1214/fit-in/1200x630/cdn.vox-cdn.com/uploads/chorus_asset/file/8792137/acastro_170629_1777_0008_v2.jpg',
          publishedAt: '2021-07-05T19:45:10Z',
          content:
            'Filed under:\r\nThe supply chain attack has reached over a thousand organizations.\r\nIllustration by Alex Castro / The Verge\r\nThree days after ransomware attackers started the holiday weekend by comprom… [+3376 chars]',
        },
        {
          source: {
            id: 'bbc-news',
            name: 'BBC News',
          },
          author: 'https://www.facebook.com/bbcnews',
          title: 'Gang behind huge cyber-attack demands $70m in Bitcoin',
          description:
            'The authors of a "colossal" ransomware attack demand the sum in Bitcoin in return for a key to unlock all files.',
          url: 'https://www.bbc.co.uk/news/technology-57719820',
          urlToImage:
            'https://ichef.bbci.co.uk/news/1024/branded_news/4532/production/_119241771_gettyimages-645051326.jpg',
          publishedAt: '2021-07-05T12:14:34Z',
          content:
            'image copyrightGetty Images\r\nThe gang behind a "colossal" ransomware attack has demanded $70m (£50.5m) paid in Bitcoin in return for a "universal decryptor" that it says will unlock the files of all … [+4140 chars]',
        },
        {
          source: {
            id: 'reuters',
            name: 'Reuters',
          },
          author: 'Reuters',
          title:
            'El Salvador to keep dollar as legal tender, seeks World Bank help with bitcoin - Reuters',
          description:
            'El Salvador will not replace the U.S. dollar with bitcoin as the legal tender, Finance Minister Alejandro Zelaya said on Wednesday, as the Central American nation sought technical assistance from the World Bank to implement bitcoin regulation.',
          url: 'https://www.reuters.com/business/el-salvador-keep-dollar-legal-tender-seeks-world-bank-help-with-bitcoin-2021-06-16/',
          urlToImage:
            'https://www.reuters.com/resizer/8_ZpjJnVb-UkP6DjxQHhV7Lywbk=/800x419/smart/filters:quality(80)/cloudfront-us-east-2.images.arcpublishing.com/reuters/UR6HS3FP5VLU3GKVDXNYGMHZFI.jpg',
          publishedAt: '2021-06-16T17:34:00Z',
          content:
            'SAN SALVADOR, June 16 (Reuters) - El Salvador will not replace the U.S. dollar with bitcoin as the legal tender, Finance Minister Alejandro Zelaya said on Wednesday, as the Central American nation so… [+1266 chars]',
        },
        {
          source: {
            id: 'reuters',
            name: 'Reuters',
          },
          author: 'Tom Arnold,Karin Strohecker',
          title:
            'El Salvador bitcoin plan "bulletproof", president says - Reuters',
          description:
            'El Salvador is determined to push ahead with making bitcoin  legal tender, a process that will bring only small risks and prove a "leap forward for humanity", the country\'s President Nayib Bukele said in an interview with a bitcoin journalist.',
          url: 'https://www.reuters.com/business/el-salvador-bitcoin-plan-bulletproof-president-says-2021-06-23/',
          urlToImage:
            'https://www.reuters.com/resizer/-NVJNngENeVucFqs_thLKomcREk=/1200x628/smart/filters:quality(80)/cloudfront-us-east-2.images.arcpublishing.com/reuters/PAJVGKERRBLV3DPA6YELYMSRTQ.jpg',
          publishedAt: '2021-06-23T13:58:00Z',
          content:
            'LONDON, June 23 (Reuters) - El Salvador is determined to push ahead with making bitcoin legal tender, a process that will bring only small risks and prove a "leap forward for humanity", the country\'s… [+2764 chars]',
        },
        {
          source: {
            id: 'reuters',
            name: 'Reuters',
          },
          author: 'Tom Arnold, Karin Strohecker',
          title:
            "El Salvador bitcoin plan 'bulletproof', president says - Reuters",
          description:
            'El Salvador is determined to push ahead with making bitcoin legal tender, a process that will bring only small risks and prove a "leap forward for humanity", the country\'s President Nayib Bukele said in an interview with a bitcoin journalist.',
          url: 'https://www.reuters.com/article/el-salvador-bitcoin-bukele-idUSL5N2O53AL',
          urlToImage:
            'https://s1.reutersmedia.net/resources_v2/images/rcom-default.png?w=800',
          publishedAt: '2021-06-23T13:46:00Z',
          content:
            'LONDON, June 23 (Reuters) - El Salvador is determined to push ahead with making bitcoin legal tender, a process that will bring only small risks and prove a leap forward for humanity, the countrys Pr… [+2648 chars]',
        },
        {
          source: {
            id: 'reuters',
            name: 'Reuters',
          },
          author: 'Reuters Staff',
          title:
            'UPDATE 1-El Salvador to keep dollar as legal tender, seeks World Bank help with bitcoin - Reuters',
          description:
            'El Salvador will not replace the U.S. dollar with bitcoin as the legal tender, Finance Minister Alejandro Zelaya said on Wednesday, as the Central American nation sought technical assistance from the World Bank to implement bitcoin regulation.',
          url: 'https://www.reuters.com/article/us-el-salvador-imf-bitcoin-idUSKCN2DS241',
          urlToImage:
            'https://static.reuters.com/resources/r/?m=02&d=20210616&t=2&i=1565932063&r=LYNXNPEH5F13P&w=800',
          publishedAt: '2021-06-16T17:20:00Z',
          content:
            'By Reuters Staff\r\nSAN SALVADOR (Reuters) - El Salvador will not replace the U.S. dollar with bitcoin as the legal tender, Finance Minister Alejandro Zelaya said on Wednesday, as the Central American … [+1110 chars]',
        },
        {
          source: {
            id: 'techcrunch',
            name: 'TechCrunch',
          },
          author: 'Natasha Mascarenhas',
          title: 'What does Uber and birth control have in common?',
          description:
            'Hello and welcome back to Equity, TechCrunch’s venture capital-focused podcast where we unpack the numbers behind the headlines. This is Equity Monday, our morning coffee chat with you that is all about the weekend, what to expect this week, and some funding …',
          url: 'http://techcrunch.com/2021/06/14/what-does-uber-and-birth-control-have-in-common/',
          urlToImage:
            'https://techcrunch.com/wp-content/uploads/2020/07/equity-podcast-2019-phone.jpg?w=711',
          publishedAt: '2021-06-14T14:48:53Z',
          content:
            'Hello and welcome back to Equity, TechCrunchs venture capital-focused podcast where we unpack the numbers behind the headlines.\r\nThis is Equity Monday, our morning coffee chat with you that is all ab… [+2045 chars]',
        },
        {
          source: {
            id: null,
            name: 'MarketBeat',
          },
          author: 'Melissa Brock',
          title:
            'Gold is Dead? Should You Opt for Gold (Over Crypto) in Your Portfolio?',
          description:
            "Bitcoin transactions are recorded on a blockchain, a distributed ledger that cannot fail. Government doesn't control bitcoin (unlike banks) and that's...",
          url: 'https://www.marketbeat.com/originals/should-you-opt-for-gold-over-crypto-in-your-portfolio/?utm_source=entrepreneurcom&amp;amp;utm_medium=entrepreneurcom',
          urlToImage:
            'https://assets.entrepreneur.com/content/3x2/2000/20160408155709-default-hero-entrepreneur.png',
          publishedAt: '2021-06-22T10:10:00Z',
          content:
            "This story originally appeared on MarketBeatWhen meme coins surged earlier this year (remember Dogecoin mania?) it might've been easy to dump everything you owned — stocks, bonds, gold — for crypto. … [+6151 chars]",
        },
        {
          source: {
            id: 'reuters',
            name: 'Reuters',
          },
          author: 'Reuters Staff',
          title: 'UPDATE 1-Bitcoin rises 9.8% to $39,035 - Reuters',
          description:
            'Bitcoin surged 9.8% to $39,035.47 on Sunday, adding $3,492.71 to its previous close.',
          url: 'https://www.reuters.com/article/crypto-currency-bitcoin-idUSL2N2NV0MV',
          urlToImage:
            'https://s1.reutersmedia.net/resources_v2/images/rcom-default.png?w=800',
          publishedAt: '2021-06-13T22:32:00Z',
          content:
            'By Reuters Staff\r\n(Adds context, background)\r\nJune 13 (Reuters) - Bitcoin surged 9.8% to $39,035.47 on Sunday, adding $3,492.71 to its previous close.\r\nBitcoin, the worlds biggest and best-known cryp… [+877 chars]',
        },
        {
          source: {
            id: 'reuters',
            name: 'Reuters',
          },
          author: 'Reuters',
          title:
            'Cryptocurrencies tumble amid China crackdown on bitcoin miners - Reuters',
          description:
            "Cryptocurrencies tumbled on Monday as China's crackdown on bitcoin mining expanded to the province of Sichuan.",
          url: 'https://www.reuters.com/technology/cryptocurrencies-tumble-amid-china-crackdown-bitcoin-miners-2021-06-21/',
          urlToImage:
            'https://www.reuters.com/resizer/vrrOc0dnUuHV9__Plp9bJglZGWs=/800x419/smart/filters:quality(80)/cloudfront-us-east-2.images.arcpublishing.com/reuters/7GDD6S7NDRPEFFFAZVABH2K454.jpg',
          publishedAt: '2021-06-21T07:12:00Z',
          content:
            "TOKYO, June 21 (Reuters) - Cryptocurrencies tumbled on Monday as China's crackdown on bitcoin mining expanded to the province of Sichuan. read more \r\nBitcoin fell to as low as $32,288 for the first t… [+377 chars]",
        },
        {
          source: {
            id: 'reuters',
            name: 'Reuters',
          },
          author: 'Tom Wilson',
          title: "Boom, bust and bewildered: Bitcoin's year so far - Reuters",
          description:
            "If you're a bitcoin investor, your nerves may have taken quite a pounding in 2021.",
          url: 'https://www.reuters.com/technology/boom-bust-bewildered-bitcoins-year-so-far-2021-06-30/',
          urlToImage:
            'https://www.reuters.com/resizer/Iz_V3_lUcgBTBIkxGaqEvdnifa0=/1200x628/smart/filters:quality(80)/cloudfront-us-east-2.images.arcpublishing.com/reuters/3GKHTWVGDVPXNFB47P2YJYB5UY.jpg',
          publishedAt: '2021-06-30T13:46:00Z',
          content:
            "A representation of virtual currency Bitcoin is seen in front of a stock graph in this illustration taken March 15, 2021. REUTERS/Dado Ruvic/IllustrationLONDON, June 30 (Reuters) - If you're a bitcoi… [+3630 chars]",
        },
        {
          source: {
            id: 'reuters',
            name: 'Reuters',
          },
          author: 'Reuters',
          title: 'Bitcoin falls 7.4 percent to $32094 - Reuters',
          description:
            'Bitcoin dropped 7.37% to $32,094.44 on Friday, losing $2,554.88 from its previous close.',
          url: 'https://www.reuters.com/technology/bitcoin-falls-74-percent-32094-2021-06-25/',
          urlToImage:
            'https://www.reuters.com/resizer/EA_FhvXIW0VXFcNDdLs7vrbpIYg=/1200x628/smart/filters:quality(80)/cloudfront-us-east-2.images.arcpublishing.com/reuters/QLML2PWULBJHRGKWO6BATZD6OY.jpg',
          publishedAt: '2021-06-25T20:21:00Z',
          content:
            'A representation of the virtual cryptocurrency Bitcoin is seen in this picture illustration taken June 14, 2021. REUTERS/Edgar Su/IllustrationJune 25 (Reuters) - Bitcoin dropped 7.37% to $32,094.44 o… [+434 chars]',
        },
      ],
      apikey: 'c4e3e8daa24a478f9043aab8dae63889',
      loading: false,
    }
  },
  methods: {
    handleClick(e) {
      this.loading = true
      if (this.search) {
        fetch(`${this.url}?q=${this.search}&apiKey=${this.apikey}`)
          .then((response) => {
            return response.json()
          })
          .then((data) => {
            this.newsCart = data.articles
            console.log(data)
            this.loading = false
          })
      }
    },
  },
}
</script>

<style lang="scss"></style>
