import requests
from bs4 import BeautifulSoup

# Từ khóa tìm kiếm
search_keyword = "danh sách học sinh"

# URL tìm kiếm của Violet
search_url = "https://violet.vn/site/search"

# Thực hiện truy vấn tìm kiếm
params = {
    "q": search_keyword,
    "search_type": "doc"  # Tìm kiếm tài liệu
}

headers = {
    "User-Agent": "Mozilla/5.0"
}

response = requests.get(search_url, params=params, headers=headers)

# Phân tích HTML
soup = BeautifulSoup(response.text, "html.parser")

# Tìm các kết quả tìm kiếm
results = soup.find_all("div", class_="doc-item")

for idx, item in enumerate(results, 1):
    title_tag = item.find("a", class_="doc-title")
    if title_tag:
        title = title_tag.text.strip()
        link = "https://violet.vn" + title_tag["href"]
        print(f"{idx}. {title}\n   {link}\n")
