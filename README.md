# Feature-identification-project
git add myfile
git commit -m "test"

! mkdir fanfics_orig

# https://archiveofourown.org/collections/GeluhsTolkienFicRecs

# https://archiveofourown.org/works?utf8=%E2%9C%93&commit=Sort+and+Filter&work_search%5Bsort_column%5D=revised_at&work_search%5Bother_tag_names%5D=&work_search%5Bexcluded_tag_names%5D=&work_search%5Bcrossover%5D=&work_search%5Bcomplete%5D=&work_search%5Bwords_from%5D=40000&work_search%5Bwords_to%5D=&work_search%5Bdate_from%5D=&work_search%5Bdate_to%5D=&work_search%5Bquery%5D=&work_search%5Blanguage_id%5D=&tag_id=The+Lord+of+the+Rings+-+All+Media+Types


fanfics = [
    'https://archiveofourown.org/works/4452956/chapters/10116950',
    'https://archiveofourown.org/works/720657/chapters/1336087',
    'https://archiveofourown.org/works/3241148/chapters/7061216',
    'https://archiveofourown.org/works/1579232/chapters/3626882',
    'https://archiveofourown.org/works/27928240/chapters/68393980',
    'https://archiveofourown.org/works/28443564/chapters/69700377',
    'https://archiveofourown.org/works/27409063/chapters/66992233',
    'https://archiveofourown.org/works/26570803/chapters/64778392',
    'https://archiveofourown.org/works/23267419/chapters/55719919',
    'https://archiveofourown.org/works/24855805/chapters/60129352',
    'https://archiveofourown.org/works/27140293/chapters/66278305',
    'https://archiveofourown.org/works/6066076/chapters/13904581',
    'https://archiveofourown.org/works/22031779/chapters/52579453',
    'https://archiveofourown.org/works/23557552/chapters/56513773',
    'https://archiveofourown.org/works/23038390/chapters/55094566',
    'https://archiveofourown.org/works/23952544/chapters/57606397',
    'https://archiveofourown.org/works/21458827/chapters/51138226',
    'https://archiveofourown.org/works/855528/chapters/1637607',
    'https://archiveofourown.org/works/3780557/chapters/8407382',
    'https://archiveofourown.org/works/11790954/chapters/26591097',
]

import AO3
from tqdm import tqdm
import time


def get_text(url):
    name = url.split('/')[-3]
    workid = AO3.utils.workid_from_url(url)
    print(f"Work ID: {workid}")
    work = AO3.Work(workid)
    # work.load_chapters()
    print(f"Chapters: {work.chapters}")

    text = ''
    for id_ in tqdm(range(1, work.chapters + 1)):
        try:
            text += work.get_chapter_text(id_)
            time.sleep(2)
        except:
            break
    with open('fanfics_orig/' + name + '.txt', 'w') as f:
        f.write(text)


for url in fanfics:
    print(url)
    get_text(url)
