---
layout: layouts/code.njk
title: code
templateClass: tmpl-post
eleventyNavigation:
  key: Test
  order: 6
---

# Add files into dataframe

import pandas as pd

books = pd.DataFrame.from_dict(uploaded, orient='index')
books.head()
