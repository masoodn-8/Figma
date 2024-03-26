# Figma
My Figma Designs
Here I'm uploading my figma drafts and designs that will help for the future references and future projects.

import scrapy

class PresidencyUniversitySpider(scrapy.Spider):
    name = "presidencyuniversity_spider"  # More descriptive name
    start_urls = ['https://presidencyuniversity.in/']

    def parse(self, response):
        title = response.css('title::text').get()
        paragraphs = response.css('p::text').getall()  # Get all paragraphs

        print("Title:", title)

        if paragraphs:  # Check if paragraphs exist to avoid empty output
            print("First Paragraph:", paragraphs[0])  # Print first paragraph
            yield {
                'title': title,
                'first_paragraph': paragraphs[0]
            }

        # Additional parsing logic for more specific content can be added here
from scrapy.crawler import CrawlerProcess

process = CrawlerProcess(settings={
    'FEED_FORMAT': 'json',
    'FEED_URI': 'output.json'
})

process.crawl(PresidencyUniversitySpider)
process.start()  # No need for process.stop() as start() handles execution
