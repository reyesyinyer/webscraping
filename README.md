{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<p style=\"text-align:center\">\n",
    "    <a href=\"https://skills.network/?utm_medium=Exinfluencer&utm_source=Exinfluencer&utm_content=000026UJ&utm_term=10006555&utm_id=NA-SkillsNetwork-Channel-SkillsNetworkCoursesIBMDeveloperSkillsNetworkPY0220ENSkillsNetwork900-2022-01-01\" target=\"_blank\">\n",
    "    <img src=\"https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/assets/logos/SN_web_lightmode.png\" width=\"200\" alt=\"Skills Network Logo\">\n",
    "    </a>\n",
    "</p>\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h1>Extracting and Visualizing Stock Data</h1>\n",
    "<h2>Description</h2>\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Extracting essential data from a dataset and displaying it is a necessary part of data science; therefore individuals can make correct decisions based on the data. In this assignment, you will extract some stock data, you will then display this data in a graph.\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h2>Table of Contents</h2>\n",
    "<div class=\"alert alert-block alert-info\" style=\"margin-top: 20px\">\n",
    "    <ul>\n",
    "        <li>Define a Function that Makes a Graph</li>\n",
    "        <li>Question 1: Use yfinance to Extract Stock Data</li>\n",
    "        <li>Question 2: Use Webscraping to Extract Tesla Revenue Data</li>\n",
    "        <li>Question 3: Use yfinance to Extract Stock Data</li>\n",
    "        <li>Question 4: Use Webscraping to Extract GME Revenue Data</li>\n",
    "        <li>Question 5: Plot Tesla Stock Graph</li>\n",
    "        <li>Question 6: Plot GameStop Stock Graph</li>\n",
    "    </ul>\n",
    "<p>\n",
    "    Estimated Time Needed: <strong>30 min</strong></p>\n",
    "</div>\n",
    "\n",
    "<hr>\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "***Note***:- If you are working Locally using anaconda, please uncomment the following code and execute it.\n",
    "Use the version as per your python version.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 1,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Collecting yfinance\n",
      "  Downloading yfinance-0.2.61-py2.py3-none-any.whl.metadata (5.8 kB)\n",
      "Requirement already satisfied: pandas>=1.3.0 in /opt/conda/lib/python3.12/site-packages (from yfinance) (2.2.3)\n",
      "Requirement already satisfied: numpy>=1.16.5 in /opt/conda/lib/python3.12/site-packages (from yfinance) (2.2.6)\n",
      "Requirement already satisfied: requests>=2.31 in /opt/conda/lib/python3.12/site-packages (from yfinance) (2.32.3)\n",
      "Collecting multitasking>=0.0.7 (from yfinance)\n",
      "  Downloading multitasking-0.0.11-py3-none-any.whl.metadata (5.5 kB)\n",
      "Requirement already satisfied: platformdirs>=2.0.0 in /opt/conda/lib/python3.12/site-packages (from yfinance) (4.3.6)\n",
      "Requirement already satisfied: pytz>=2022.5 in /opt/conda/lib/python3.12/site-packages (from yfinance) (2024.2)\n",
      "Requirement already satisfied: frozendict>=2.3.4 in /opt/conda/lib/python3.12/site-packages (from yfinance) (2.4.6)\n",
      "Collecting peewee>=3.16.2 (from yfinance)\n",
      "  Downloading peewee-3.18.1.tar.gz (3.0 MB)\n",
      "\u001b[2K     \u001b[90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━\u001b[0m \u001b[32m3.0/3.0 MB\u001b[0m \u001b[31m96.9 MB/s\u001b[0m eta \u001b[36m0:00:00\u001b[0m\n",
      "  Installing build dependencies ... \u001b[?2done\n",
      "\u001b[?25h  Getting requirements to build wheel ... \u001b[?25ldone\n",
      "\u001b[?25h  Preparing metadata (pyproject.toml) ... \u001b[?25ldone\n",
      "\u001b[?25hRequirement already satisfied: beautifulsoup4>=4.11.1 in /opt/conda/lib/python3.12/site-packages (from yfinance) (4.12.3)\n",
      "Collecting curl_cffi>=0.7 (from yfinance)\n",
      "  Downloading curl_cffi-0.11.1-cp39-abi3-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (14 kB)\n",
      "Collecting protobuf>=3.19.0 (from yfinance)\n",
      "  Downloading protobuf-6.31.1-cp39-abi3-manylinux2014_x86_64.whl.metadata (593 bytes)\n",
      "Collecting websockets>=13.0 (from yfinance)\n",
      "  Downloading websockets-15.0.1-cp312-cp312-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (6.8 kB)\n",
      "Requirement already satisfied: soupsieve>1.2 in /opt/conda/lib/python3.12/site-packages (from beautifulsoup4>=4.11.1->yfinance) (2.5)\n",
      "Requirement already satisfied: cffi>=1.12.0 in /opt/conda/lib/python3.12/site-packages (from curl_cffi>=0.7->yfinance) (1.17.1)\n",
      "Requirement already satisfied: certifi>=2024.2.2 in /opt/conda/lib/python3.12/site-packages (from curl_cffi>=0.7->yfinance) (2024.12.14)\n",
      "Requirement already satisfied: python-dateutil>=2.8.2 in /opt/conda/lib/python3.12/site-packages (from pandas>=1.3.0->yfinance) (2.9.0.post0)\n",
      "Requirement already satisfied: tzdata>=2022.7 in /opt/conda/lib/python3.12/site-packages (from pandas>=1.3.0->yfinance) (2025.2)\n",
      "Requirement already satisfied: charset_normalizer<4,>=2 in /opt/conda/lib/python3.12/site-packages (from requests>=2.31->yfinance) (3.4.1)\n",
      "Requirement already satisfied: idna<4,>=2.5 in /opt/conda/lib/python3.12/site-packages (from requests>=2.31->yfinance) (3.10)\n",
      "Requirement already satisfied: urllib3<3,>=1.21.1 in /opt/conda/lib/python3.12/site-packages (from requests>=2.31->yfinance) (2.3.0)\n",
      "Requirement already satisfied: pycparser in /opt/conda/lib/python3.12/site-packages (from cffi>=1.12.0->curl_cffi>=0.7->yfinance) (2.22)\n",
      "Requirement already satisfied: six>=1.5 in /opt/conda/lib/python3.12/site-packages (from python-dateutil>=2.8.2->pandas>=1.3.0->yfinance) (1.17.0)\n",
      "Downloading yfinance-0.2.61-py2.py3-none-any.whl (117 kB)\n",
      "Downloading curl_cffi-0.11.1-cp39-abi3-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (8.5 MB)\n",
      "\u001b[2K   \u001b[90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━\u001b[0m \u001b[32m8.5/8.5 MB\u001b[0m \u001b[31m111.0 MB/s\u001b[0m eta \u001b[36m0:00:00\u001b[0m\n",
      "\u001b[?25hDownloading multitasking-0.0.11-py3-none-any.whl (8.5 kB)\n",
      "Downloading protobuf-6.31.1-cp39-abi3-manylinux2014_x86_64.whl (321 kB)\n",
      "Downloading websockets-15.0.1-cp312-cp312-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl (182 kB)\n",
      "Building wheels for collected packages: peewee\n",
      "  Building wheel for peewee (pyproject.toml) ... \u001b[?done\n",
      "\u001b[?25h  Created wheel for peewee: filename=peewee-3.18.1-cp312-cp312-linux_x86_64.whl size=303801 sha256=de8bf48983c5267baf709760f0d7b14efbe376314039526fcc4f3d9d8edfe064\n",
      "  Stored in directory: /home/jupyterlab/.cache/pip/wheels/1a/57/6a/bb71346381d0d911cd4ce3026f1fa720da76707e4f01cf27dd\n",
      "Successfully built peewee\n",
      "Installing collected packages: peewee, multitasking, websockets, protobuf, curl_cffi, yfinance\n",
      "Successfully installed curl_cffi-0.11.1 multitasking-0.0.11 peewee-3.18.1 protobuf-6.31.1 websockets-15.0.1 yfinance-0.2.61\n",
      "Requirement already satisfied: bs4 in /opt/conda/lib/python3.12/site-packages (0.0.2)\n",
      "Requirement already satisfied: beautifulsoup4 in /opt/conda/lib/python3.12/site-packages (from bs4) (4.12.3)\n",
      "Requirement already satisfied: soupsieve>1.2 in /opt/conda/lib/python3.12/site-packages (from beautifulsoup4->bs4) (2.5)\n",
      "Requirement already satisfied: nbformat in /opt/conda/lib/python3.12/site-packages (5.10.4)\n",
      "Requirement already satisfied: fastjsonschema>=2.15 in /opt/conda/lib/python3.12/site-packages (from nbformat) (2.21.1)\n",
      "Requirement already satisfied: jsonschema>=2.6 in /opt/conda/lib/python3.12/site-packages (from nbformat) (4.23.0)\n",
      "Requirement already satisfied: jupyter-core!=5.0.*,>=4.12 in /opt/conda/lib/python3.12/site-packages (from nbformat) (5.7.2)\n",
      "Requirement already satisfied: traitlets>=5.1 in /opt/conda/lib/python3.12/site-packages (from nbformat) (5.14.3)\n",
      "Requirement already satisfied: attrs>=22.2.0 in /opt/conda/lib/python3.12/site-packages (from jsonschema>=2.6->nbformat) (25.1.0)\n",
      "Requirement already satisfied: jsonschema-specifications>=2023.03.6 in /opt/conda/lib/python3.12/site-packages (from jsonschema>=2.6->nbformat) (2024.10.1)\n",
      "Requirement already satisfied: referencing>=0.28.4 in /opt/conda/lib/python3.12/site-packages (from jsonschema>=2.6->nbformat) (0.36.2)\n",
      "Requirement already satisfied: rpds-py>=0.7.1 in /opt/conda/lib/python3.12/site-packages (from jsonschema>=2.6->nbformat) (0.22.3)\n",
      "Requirement already satisfied: platformdirs>=2.5 in /opt/conda/lib/python3.12/site-packages (from jupyter-core!=5.0.*,>=4.12->nbformat) (4.3.6)\n",
      "Requirement already satisfied: typing-extensions>=4.4.0 in /opt/conda/lib/python3.12/site-packages (from referencing>=0.28.4->jsonschema>=2.6->nbformat) (4.12.2)\n",
      "Requirement already satisfied: plotly in /opt/conda/lib/python3.12/site-packages (5.24.1)\n",
      "Collecting plotly\n",
      "  Downloading plotly-6.1.2-py3-none-any.whl.metadata (6.9 kB)\n",
      "Collecting narwhals>=1.15.1 (from plotly)\n",
      "  Downloading narwhals-1.41.0-py3-none-any.whl.metadata (11 kB)\n",
      "Requirement already satisfied: packaging in /opt/conda/lib/python3.12/site-packages (from plotly) (24.2)\n",
      "Downloading plotly-6.1.2-py3-none-any.whl (16.3 MB)\n",
      "\u001b[2K   \u001b[90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━\u001b[0m \u001b[32m16.3/16.3 MB\u001b[0m \u001b[31m162.3 MB/s\u001b[0m eta \u001b[36m0:00:00\u001b[0m\n",
      "\u001b[?25hDownloading narwhals-1.41.0-py3-none-any.whl (357 kB)\n",
      "Installing collected packages: narwhals, plotly\n",
      "  Attempting uninstall: plotly\n",
      "    Found existing installation: plotly 5.24.1\n",
      "    Uninstalling plotly-5.24.1:\n",
      "      Successfully uninstalled plotly-5.24.1\n",
      "Successfully installed narwhals-1.41.0 plotly-6.1.2\n"
     ]
    }
   ],
   "source": [
    "!pip install yfinance\n",
    "!pip install bs4\n",
    "!pip install nbformat\n",
    "!pip install --upgrade plotly"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": [
    "import yfinance as yf\n",
    "import pandas as pd\n",
    "import requests\n",
    "from bs4 import BeautifulSoup\n",
    "import plotly.graph_objects as go\n",
    "from plotly.subplots import make_subplots"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "jupyter": {
     "source_hidden": true
    }
   },
   "outputs": [],
   "source": [
    "import plotly.io as pio\n",
    "pio.renderers.default = \"iframe\""
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "In Python, you can ignore warnings using the warnings module. You can use the filterwarnings function to filter or ignore specific warning messages or categories.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "metadata": {},
   "outputs": [],
   "source": [
    "import warnings\n",
    "# Ignore all warnings\n",
    "warnings.filterwarnings(\"ignore\", category=FutureWarning)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Define Graphing Function\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "In this section, we define the function `make_graph`. **You don't have to know how the function works, you should only care about the inputs. It takes a dataframe with stock data (dataframe must contain Date and Close columns), a dataframe with revenue data (dataframe must contain Date and Revenue columns), and the name of the stock.**\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "metadata": {},
   "outputs": [],
   "source": [
    "def make_graph(stock_data, revenue_data, stock):\n",
    "    fig = make_subplots(rows=2, cols=1, shared_xaxes=True, subplot_titles=(\"Historical Share Price\", \"Historical Revenue\"), vertical_spacing = .3)\n",
    "    stock_data_specific = stock_data[stock_data.Date <= '2021-06-14']\n",
    "    revenue_data_specific = revenue_data[revenue_data.Date <= '2021-04-30']\n",
    "    fig.add_trace(go.Scatter(x=pd.to_datetime(stock_data_specific.Date, infer_datetime_format=True), y=stock_data_specific.Close.astype(\"float\"), name=\"Share Price\"), row=1, col=1)\n",
    "    fig.add_trace(go.Scatter(x=pd.to_datetime(revenue_data_specific.Date, infer_datetime_format=True), y=revenue_data_specific.Revenue.astype(\"float\"), name=\"Revenue\"), row=2, col=1)\n",
    "    fig.update_xaxes(title_text=\"Date\", row=1, col=1)\n",
    "    fig.update_xaxes(title_text=\"Date\", row=2, col=1)\n",
    "    fig.update_yaxes(title_text=\"Price ($US)\", row=1, col=1)\n",
    "    fig.update_yaxes(title_text=\"Revenue ($US Millions)\", row=2, col=1)\n",
    "    fig.update_layout(showlegend=False,\n",
    "    height=900,\n",
    "    title=stock,\n",
    "    xaxis_rangeslider_visible=True)\n",
    "    fig.show()\n",
    "    from IPython.display import display, HTML\n",
    "    fig_html = fig.to_html()\n",
    "    display(HTML(fig_html))"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Use the make_graph function that we’ve already defined. You’ll need to invoke it in questions 5 and 6 to display the graphs and create the dashboard. \n",
    "> **Note: You don’t need to redefine the function for plotting graphs anywhere else in this notebook; just use the existing function.**\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Question 1: Use yfinance to Extract Stock Data\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Using the `Ticker` function enter the ticker symbol of the stock we want to extract data on to create a ticker object. The stock is Tesla and its ticker symbol is `TSLA`.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "metadata": {},
   "outputs": [],
   "source": [
    "import yfinance as yf\n",
    "\n",
    "# Crear el objeto ticker para Tesla\n",
    "tesla_ticker = yf.Ticker(\"TSLA\")\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Using the ticker object and the function `history` extract stock information and save it in a dataframe named `tesla_data`. Set the `period` parameter to ` \"max\" ` so we get information for the maximum amount of time.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 6,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "                               Open      High       Low     Close     Volume  \\\n",
      "Date                                                                           \n",
      "2010-06-29 00:00:00-04:00  1.266667  1.666667  1.169333  1.592667  281494500   \n",
      "2010-06-30 00:00:00-04:00  1.719333  2.028000  1.553333  1.588667  257806500   \n",
      "2010-07-01 00:00:00-04:00  1.666667  1.728000  1.351333  1.464000  123282000   \n",
      "2010-07-02 00:00:00-04:00  1.533333  1.540000  1.247333  1.280000   77097000   \n",
      "2010-07-06 00:00:00-04:00  1.333333  1.333333  1.055333  1.074000  103003500   \n",
      "\n",
      "                           Dividends  Stock Splits  \n",
      "Date                                                \n",
      "2010-06-29 00:00:00-04:00        0.0           0.0  \n",
      "2010-06-30 00:00:00-04:00        0.0           0.0  \n",
      "2010-07-01 00:00:00-04:00        0.0           0.0  \n",
      "2010-07-02 00:00:00-04:00        0.0           0.0  \n",
      "2010-07-06 00:00:00-04:00        0.0           0.0  \n"
     ]
    }
   ],
   "source": [
    "import yfinance as yf\n",
    "\n",
    "# Crear el objeto ticker para Tesla\n",
    "tesla_ticker = yf.Ticker(\"TSLA\")\n",
    "\n",
    "# Extraer datos históricos y guardarlos en un DataFrame\n",
    "tesla_data = tesla_ticker.history(period=\"max\")\n",
    "\n",
    "# Mostrar las primeras filas del DataFrame\n",
    "print(tesla_data.head())\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "**Reset the index** using the `reset_index(inplace=True)` function on the tesla_data DataFrame and display the first five rows of the `tesla_data` dataframe using the `head` function. Take a screenshot of the results and code from the beginning of Question 1 to the results below.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "                       Date      Open      High       Low     Close  \\\n",
      "0 2010-06-29 00:00:00-04:00  1.266667  1.666667  1.169333  1.592667   \n",
      "1 2010-06-30 00:00:00-04:00  1.719333  2.028000  1.553333  1.588667   \n",
      "2 2010-07-01 00:00:00-04:00  1.666667  1.728000  1.351333  1.464000   \n",
      "3 2010-07-02 00:00:00-04:00  1.533333  1.540000  1.247333  1.280000   \n",
      "4 2010-07-06 00:00:00-04:00  1.333333  1.333333  1.055333  1.074000   \n",
      "\n",
      "      Volume  Dividends  Stock Splits  \n",
      "0  281494500        0.0           0.0  \n",
      "1  257806500        0.0           0.0  \n",
      "2  123282000        0.0           0.0  \n",
      "3   77097000        0.0           0.0  \n",
      "4  103003500        0.0           0.0  \n"
     ]
    }
   ],
   "source": [
    "# Restablecer el índice\n",
    "tesla_data.reset_index(inplace=True)\n",
    "\n",
    "# Mostrar las primeras cinco filas\n",
    "print(tesla_data.head(5))\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Question 2: Use Webscraping to Extract Tesla Revenue Data\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Use the `requests` library to download the webpage https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/revenue.htm Save the text of the response as a variable named `html_data`.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 8,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "<?xml version=\"1.0\" encoding=\"UTF-8\" standalone=\"yes\"?><Error><Code>NoSuchKey</Code><Message>The specified key does not exist.</Message><Resource>/cf-courses-data/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/revenue.html</Resource><RequestId>45873d9f-d5bd-4610-ae9a-d889fcc54a66</RequestId><httpStatusCode>404</httpStatusCode></Error>\n"
     ]
    }
   ],
   "source": [
    "import requests\n",
    "\n",
    "# URL de la página con los datos\n",
    "url = \"https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/revenue.html\"\n",
    "\n",
    "# Descargar la página web\n",
    "response = requests.get(url)\n",
    "\n",
    "# Guardar el contenido en una variable\n",
    "html_data = response.text\n",
    "\n",
    "# Mostrar una vista previa del contenido\n",
    "print(html_data[:500])  # Muestra los primeros 500 caracteres\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Parse the html data using `beautiful_soup` using parser i.e `html5lib` or `html.parser`.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 9,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "<?xml version=\"1.0\" encoding=\"UTF-8\" standalone=\"yes\"?>\n",
      "<error>\n",
      " <code>\n",
      "  NoSuchKey\n",
      " </code>\n",
      " <message>\n",
      "  The specified key does not exist.\n",
      " </message>\n",
      " <resource>\n",
      "  /cf-courses-data/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/revenue.html\n",
      " </resource>\n",
      " <requestid>\n",
      "  45873d9f-d5bd-4610-ae9a-d889fcc54a66\n",
      " </requestid>\n",
      " <httpstatuscode>\n",
      "  404\n",
      " </httpstatuscode>\n",
      "</error>\n",
      "\n"
     ]
    },
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "/opt/conda/lib/python3.12/html/parser.py:171: XMLParsedAsHTMLWarning: It looks like you're parsing an XML document using an HTML parser. If this really is an HTML document (maybe it's XHTML?), you can ignore or filter this warning. If it's XML, you should know that using an XML parser will be more reliable. To parse this document as XML, make sure you have the lxml package installed, and pass the keyword argument `features=\"xml\"` into the BeautifulSoup constructor.\n",
      "  k = self.parse_starttag(i)\n"
     ]
    }
   ],
   "source": [
    "from bs4 import BeautifulSoup\n",
    "\n",
    "# Analizar el HTML con html.parser\n",
    "soup = BeautifulSoup(html_data, \"html.parser\")\n",
    "\n",
    "# O usar html5lib\n",
    "# soup = BeautifulSoup(html_data, \"html5lib\")\n",
    "\n",
    "# Mostrar una vista previa del contenido analizado\n",
    "print(soup.prettify()[:500])  # Muestra los primeros 500 caracteres\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Using `BeautifulSoup` or the `read_html` function extract the table with `Tesla Revenue` and store it into a dataframe named `tesla_revenue`. The dataframe should have columns `Date` and `Revenue`.\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<details><summary>Step-by-step instructions</summary>\n",
    "\n",
    "```\n",
    "\n",
    "Here are the step-by-step instructions:\n",
    "\n",
    "1. Create an Empty DataFrame\n",
    "2. Find the Relevant Table\n",
    "3. Check for the Tesla Quarterly Revenue Table\n",
    "4. Iterate Through Rows in the Table Body\n",
    "5. Extract Data from Columns\n",
    "6. Append Data to the DataFrame\n",
    "\n",
    "```\n",
    "</details>\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<details><summary>Click here if you need help locating the table</summary>\n",
    "\n",
    "```\n",
    "    \n",
    "Below is the code to isolate the table, you will now need to loop through the rows and columns like in the previous lab\n",
    "    \n",
    "soup.find_all(\"tbody\")[1]\n",
    "    \n",
    "If you want to use the read_html function the table is located at index 1\n",
    "\n",
    "We are focusing on quarterly revenue in the lab.\n",
    "```\n",
    "\n",
    "</details>\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": [
    "import pandas as pd\n",
    "\n",
    "# Crear un DataFrame vacío con columnas Date y Revenue\n",
    "tesla_revenue = pd.DataFrame(columns=[\"Date\", \"Revenue\"])\n",
    "import requests\n",
    "\n",
    "\n",
    "# URL de la página\n",
    "url = \"https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/revenue.html\"\n",
    "\n",
    "# Realizar la solicitud HTTP\n",
    "response = requests.get(url)\n",
    "\n",
    "# Guardar el contenido HTML de la página\n",
    "html_data = response.text\n",
    "\n",
    "from bs4 import BeautifulSoup\n",
    "\n",
    "# Analizar el HTML con BeautifulSoup\n",
    "soup = BeautifulSoup(html_data, \"html.parser\")\n",
    "\n",
    "# Encontrar todas las tablas en el HTML\n",
    "tables = soup.find_all(\"table\")\n",
    "\n",
    "# Suponiendo que la primera tabla sea la correcta (podemos ajustar si es necesario)\n",
    "tesla_table = tables[0]\n",
    "\n",
    "# Iterar a través de las filas del cuerpo de la tabla\n",
    "rows = tesla_table.find_all(\"tr\")\n",
    "\n",
    "for row in rows[1:]:  # Omitir la primera fila si es el encabezado\n",
    "    cols = row.find_all(\"td\")\n",
    "    if len(cols) == 2:  # Asegurar que la fila tiene dos columnas\n",
    "        date = cols[0].text.strip()\n",
    "        revenue = cols[1].text.strip()\n",
    "        tesla_revenue = tesla_revenue.append({\"Date\": date, \"Revenue\": revenue}, ignore_index=True)\n",
    "\n",
    "print(tesla_revenue.head())\n",
    "\n",
    "\n",
    "\n",
    "\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Execute the following line to remove the comma and dollar sign from the `Revenue` column. \n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": [
    "tesla_revenue[\"Revenue\"] = tesla_revenue['Revenue'].str.replace(',|\\$',\"\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Execute the following lines to remove an null or empty strings in the Revenue column.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": [
    "tesla_revenue.dropna(inplace=True)\n",
    "\n",
    "tesla_revenue = tesla_revenue[tesla_revenue['Revenue'] != \"\"]"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Display the last 5 row of the `tesla_revenue` dataframe using the `tail` function. Take a screenshot of the results.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": [
    "# Mostrar las últimas 5 filas del DataFrame\n",
    "print(tesla_revenue.tail(5))\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Question 3: Use yfinance to Extract Stock Data\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Using the `Ticker` function enter the ticker symbol of the stock we want to extract data on to create a ticker object. The stock is GameStop and its ticker symbol is `GME`.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": [
    "import yfinance as yf\n",
    "\n",
    "# Crear el objeto ticker para GameStop\n",
    "gamestop_ticker = yf.Ticker(\"GME\")\n",
    "\n",
    "# Mostrar información básica del objeto\n",
    "print(gamestop_ticker.info)\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Using the ticker object and the function `history` extract stock information and save it in a dataframe named `gme_data`. Set the `period` parameter to ` \"max\" ` so we get information for the maximum amount of time.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": [
    "import yfinance as yf\n",
    "\n",
    "# Crear el objeto ticker para GameStop\n",
    "gamestop_ticker = yf.Ticker(\"GME\")\n",
    "\n",
    "# Extraer datos históricos y guardarlos en un DataFrame\n",
    "gme_data = gamestop_ticker.history(period=\"max\")\n",
    "\n",
    "# Mostrar las primeras filas del DataFrame\n",
    "print(gme_data.head())\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "**Reset the index** using the `reset_index(inplace=True)` function on the gme_data DataFrame and display the first five rows of the `gme_data` dataframe using the `head` function. Take a screenshot of the results and code from the beginning of Question 3 to the results below.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": [
    "# Restablecer el índice\n",
    "gme_data.reset_index(inplace=True)\n",
    "\n",
    "# Mostrar las primeras cinco filas\n",
    "print(gme_data.head(5))\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Question 4: Use Webscraping to Extract GME Revenue Data\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Use the `requests` library to download the webpage https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/stock.html. Save the text of the response as a variable named `html_data_2`.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": [
    "import requests\n",
    "\n",
    "# URL de la página con los datos de ingresos de GameStop\n",
    "url = \"https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/stock.html\"\n",
    "\n",
    "# Descargar la página web\n",
    "response = requests.get(url)\n",
    "\n",
    "# Guardar el contenido en una variable\n",
    "html_data_2 = response.text\n",
    "\n",
    "# Mostrar una vista previa del contenido\n",
    "print(html_data_2[:500])  # Muestra los primeros 500 caracteres\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Parse the html data using `beautiful_soup` using parser i.e `html5lib` or `html.parser`.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": [
    "from bs4 import BeautifulSoup\n",
    "\n",
    "# Analizar el HTML con html.parser\n",
    "soup = BeautifulSoup(html_data_2, \"html.parser\")\n",
    "\n",
    "# O usar html5lib\n",
    "# soup = BeautifulSoup(html_data_2, \"html5lib\")\n",
    "\n",
    "# Mostrar una vista previa del contenido analizado\n",
    "print(soup.prettify()[:500])  # Muestra los primeros 500 caracteres\n",
    "\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Using `BeautifulSoup` or the `read_html` function extract the table with `GameStop Revenue` and store it into a dataframe named `gme_revenue`. The dataframe should have columns `Date` and `Revenue`. Make sure the comma and dollar sign is removed from the `Revenue` column.\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "> **Note: Use the method similar to what you did in question 2.**  \n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<details><summary>Click here if you need help locating the table</summary>\n",
    "\n",
    "```\n",
    "    \n",
    "Below is the code to isolate the table, you will now need to loop through the rows and columns like in the previous lab\n",
    "    \n",
    "soup.find_all(\"tbody\")[1]\n",
    "    \n",
    "If you want to use the read_html function the table is located at index 1\n",
    "\n",
    "\n",
    "```\n",
    "\n",
    "</details>\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": [
    "import requests\n",
    "from bs4 import BeautifulSoup\n",
    "import pandas as pd\n",
    "\n",
    "# URL de la página con los datos de ingresos de GameStop\n",
    "url = \"https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/stock.html\"\n",
    "\n",
    "# Descargar el contenido de la página web\n",
    "response = requests.get(url)\n",
    "html_data_2 = response.text\n",
    "\n",
    "# Analizar el HTML con BeautifulSoup\n",
    "soup = BeautifulSoup(html_data_2, \"html.parser\")\n",
    "\n",
    "# Encontrar la tabla con los ingresos de GameStop\n",
    "table = soup.find(\"table\")  # Ajusta el selector si es necesario\n",
    "\n",
    "# Convertir la tabla en un DataFrame de pandas\n",
    "gme_revenue = pd.read_html(str(table))[0]\n",
    "\n",
    "# Renombrar columnas para que coincidan con \"Date\" y \"Revenue\"\n",
    "gme_revenue.columns = [\"Date\", \"Revenue\"]\n",
    "\n",
    "# Eliminar la coma y el signo de dólar de la columna Revenue\n",
    "gme_revenue[\"Revenue\"] = gme_revenue[\"Revenue\"].replace({\"\\\\$\": \"\", \",\": \"\"}, regex=True)\n",
    "\n",
    "# Mostrar las primeras filas del DataFrame\n",
    "print(gme_revenue.head())\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Display the last five rows of the `gme_revenue` dataframe using the `tail` function. Take a screenshot of the results.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": [
    "# Mostrar las últimas 5 filas del DataFrame\n",
    "print(gme_revenue.tail(5))\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": [
    "## Question 5: Plot Tesla Stock Graph\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Use the `make_graph` function to graph the Tesla Stock Data, also provide a title for the graph. Note the graph will only show data upto June 2021.\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<details><summary>Hint</summary>\n",
    "\n",
    "```\n",
    "\n",
    "You just need to invoke the make_graph function with the required parameter to print the graphs.The structure to call the `make_graph` function is `make_graph(tesla_data, tesla_revenue, 'Tesla')`.\n",
    "\n",
    "```\n",
    "    \n",
    "</details>\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": [
    "import plotly.graph_objects as go\n",
    "from plotly.subplots import make_subplots\n",
    "\n",
    "# Definir la función para graficar\n",
    "def make_graph(stock_data, revenue_data, stock):\n",
    "    fig = make_subplots(rows=2, cols=1, shared_xaxes=True, \n",
    "                        subplot_titles=(\"Historical Share Price\", \"Historical Revenue\"), \n",
    "                        vertical_spacing=0.3)\n",
    "\n",
    "    # Filtrar datos hasta junio de 2021\n",
    "    stock_data_specific = stock_data[stock_data.Date <= \"2021-06-14\"]\n",
    "    revenue_data_specific = revenue_data[revenue_data.Date <= \"2021-04-30\"]\n",
    "\n",
    "    # Agregar trazas al gráfico\n",
    "    fig.add_trace(go.Scatter(x=pd.to_datetime(stock_data_specific.Date, infer_datetime_format=True), \n",
    "                             y=stock_data_specific.Close.astype(\"float\"), \n",
    "                             name=\"Share Price\"), row=1, col=1)\n",
    "\n",
    "    fig.add_trace(go.Scatter(x=pd.to_datetime(revenue_data_specific.Date, infer_datetime_format=True), \n",
    "                             y=revenue_data_specific.Revenue.astype(\"float\"), \n",
    "                             name=\"Revenue\"), row=2, col=1)\n",
    "\n",
    "    # Configurar etiquetas de ejes\n",
    "    fig.update_xaxes(title_text=\"Date\", row=1, col=1)\n",
    "    fig.update_xaxes(title_text=\"Date\", row=2, col=1)\n",
    "    fig.update_yaxes(title_text=\"Price ($US)\", row=1, col=1)\n",
    "    fig.update_yaxes(title_text=\"Revenue ($US Millions)\", row=2, col=1)\n",
    "\n",
    "    # Configurar título y mostrar gráfico\n",
    "    fig.update_layout(showlegend=False, height=900, title=stock, xaxis_rangeslider_visible=True)\n",
    "    fig.show()\n",
    "\n",
    "# Llamar a la función con los datos de Tesla\n",
    "make_graph(tesla_data, tesla_revenue, \"Tesla Stock Data\")\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Question 6: Plot GameStop Stock Graph\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Use the `make_graph` function to graph the GameStop Stock Data, also provide a title for the graph. The structure to call the `make_graph` function is `make_graph(gme_data, gme_revenue, 'GameStop')`. Note the graph will only show data upto June 2021.\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<details><summary>Hint</summary>\n",
    "\n",
    "```\n",
    "\n",
    "You just need to invoke the make_graph function with the required parameter to print the graphs.The structure to call the `make_graph` function is `make_graph(gme_data, gme_revenue, 'GameStop')`\n",
    "\n",
    "```\n",
    "    \n",
    "</details>\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": [
    "# Graficar los datos de GameStop\n",
    "make_graph(gme_data, gme_revenue, \"GameStop\")\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h2>About the Authors:</h2> \n",
    "\n",
    "<a href=\"https://www.linkedin.com/in/joseph-s-50398b136/\">Joseph Santarcangelo</a> has a PhD in Electrical Engineering, his research focused on using machine learning, signal processing, and computer vision to determine how videos impact human cognition. Joseph has been working for IBM since he completed his PhD.\n",
    "\n",
    "Azim Hirjani\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Change Log\n",
    "\n",
    "| Date (YYYY-MM-DD) | Version | Changed By    | Change Description        |\n",
    "| ----------------- | ------- | ------------- | ------------------------- |\n",
    "| 2022-02-28        | 1.2     | Lakshmi Holla | Changed the URL of GameStop |\n",
    "| 2020-11-10        | 1.1     | Malika Singla | Deleted the Optional part |\n",
    "| 2020-08-27        | 1.0     | Malika Singla | Added lab to GitLab       |\n",
    "\n",
    "<hr>\n",
    "\n",
    "## <h3 align=\"center\"> © IBM Corporation 2020. All rights reserved. <h3/>\n",
    "\n",
    "<p>\n"
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3 (ipykernel)",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.12.8"
  },
  "prev_pub_hash": "847bbe99ddd9f2dc606aa9f731e386824fa521d0c7e38672c5f080f5d71a8326"
 },
 "nbformat": 4,
 "nbformat_minor": 4
}
