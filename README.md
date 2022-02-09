import scrapy

class Assessment(scrapy.Spider):
    name='quotes'

    def start_requests(self):
        urls=['https://www.carbon38.com//shop-all-activewear//tops',
                      'https://carbon38.com//collections//tops//page=3']

        for url in urls:
            yield scrapy.Request(url=urls, callback=self.parse)

    def parse(self,response):
        page=response.url.split("/")[-2]
        filename='quotes-as.html' % page
        with open(filename,'wb') as f:
            f.write(response.body)
            self.log('saved file as' % filename)
