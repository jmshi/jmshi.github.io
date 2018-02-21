---
id: 270
title: games and twitter
date: 2016-10-31T01:05:01+00:00
author: jiming5_wp
layout: post
guid: http://jimingshi.us/?page_id=270
permalink: /games-and-twitter/
image: /wp-content/uploads/2016/10/bird_nest.png
categories:
  - Data Science
tags:
  - twitter
  - natural language processing
---
games\_and\_tweets


  


<!-- Custom stylesheet, it must be in the same directory as the html file -->

<!-- Loading mathjax macro -->


  
<!-- Load mathjax -->


  

  
<!-- MathJax configuration -->


  

  
<!-- End of mathjax configuration -->

<div id="notebook" class="border-box-sizing" tabindex="-1">
  <div id="notebook-container" class="container">
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [16]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython2">
              <pre><span class="kn">from</span> <span class="nn">IPython.display</span> <span class="kn">import</span> <span class="n">HTML</span>
<span class="n">HTML</span><span class="p">(</span><span class="s1">'''&lt;script&gt;</span>
<span class="s1">code_show=true; </span>
<span class="s1">function code_toggle() {</span>
<span class="s1"> if (code_show){</span>
<span class="s1"> $('div.input').hide();</span>
<span class="s1"> } else {</span>
<span class="s1"> $('div.input').show();</span>
<span class="s1"> }</span>
<span class="s1"> code_show = !code_show</span>
<span class="s1">} </span>
<span class="s1">$( document ).ready(code_toggle);</span>
<span class="s1">&lt;/script&gt;</span>
<span class="s1">The raw code for this IPython notebook is by default hidden for easier reading.</span>
<span class="s1">To toggle on/off the raw code, click &lt;a href="javascript:code_toggle()"&gt;here&lt;/a&gt;.'''</span><span class="p">)</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt output_prompt">
              Out[16]:
            </div>
            
            <div class="output_html rendered_html output_subarea output_execute_result">
              <br /> The raw code for this IPython notebook is by default hidden for easier reading.<br /> To toggle on/off the raw code, click <button type="button" onclick="code_toggle();">Here</button>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <h1 id="1.-Introductio">
            1. Introduction<a class="anchor-link" href="#1.-Introductio">¶</a>
          </h1>
          
          <p>
            <strong>Motivation:</strong>  <img class="size-medium wp-image-273 alignright" src="http://jimingshi.us/wp-content/uploads/2016/10/bird_nest-300x300.png" alt="bird_nest" width="400" height="400" srcset="http://jimingshi.us/wp-content/uploads/2016/10/bird_nest-300x300.png 300w, http://jimingshi.us/wp-content/uploads/2016/10/bird_nest-150x150.png 150w, http://jimingshi.us/wp-content/uploads/2016/10/bird_nest.png 420w" sizes="(max-width: 400px) 100vw, 400px" />Along with the explosion of popularity of mobile devices, mobile games also become more and more popular nowadays. From retro games such as Plants vs. Zombies and Flappy Bird to more recent multiplayer games such as Clash of Clans and Pokemon Go, there are a variety of them which all made big success but with very different strategies.Investigating how popular they are and what make them popular or not would bring instructional information which is invaluable to determine a better short/long term plan of their product and service.
          </p>
          
          <p>
            Text mining via social media such as Twitter comes in handy in this kind of task. As Twitter data constitutes a rich source of information about any topic imaginable, they can be used to find trends related to a specific keyword, measuring brand sentiment, and gathering feedback about new products and services.
          </p>
          
          <p>
            In this proposal, I will demonstrate the possibility to use Twitter to (1) make very efficient and productive survey in the mobile game business, and (2) perform detailed analysis on given product (here use Pokemon Go as an example) to find out important information such as hot terms/topic, product usage patterns, and the customer sentiment of the product.
          </p>
          
          <p>
            <strong>Methods/Tools</strong>: I use <a href="https://dev.twitter.com/streaming/overview">Twitter Streaming API</a> together with Python libraries such as <a href="http://www.tweepy.org/">$\texttt{Tweepy}$</a> and <a href="https://pypi.python.org/pypi/twitterscraper">$\texttt{twitterscraper}$</a> to collect user information and relevant tweets (in the past 1-2 weeks) about certain set of popular mobile games. Use Natural Language Processing libraries such as $\texttt{NLTK}$ to find keywords which characterize the game, and use $\texttt{matplotlib}$ and $\texttt{Vincent}$ to render plots.
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <h1 id="2.-Data-collection">
            2. Data collection<a class="anchor-link" href="#2.-Data-collection">¶</a>
          </h1>
          
          <ul>
            <li>
              For the popularity survey, I first use Twitter Streaming API together with Python libraries to extract user information, such as number of followers, created time, and number of likes, from the official twitter account of a list of 14 most popular mobile games, based on internet reviews in 2015 and 2016.
            </li>
            <li>
              I then collect all tweets that are related to each game in the past week (Oct-23 to Oct-29, 2016) using web scraping library twitterscraper. This results in about 120K tweets in total.
            </li>
            <li>
              In order to perform more detailed study of a given mobile game, I pick the most popular game Pokemon Go as an example, and expand the data set to include all tweets within the past two weeks. That gives a total tweets count about 120K for Pokemon Go alone.
            </li>
          </ul>
          
          <p>
            &nbsp;
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <h1 id="3.-Popularity-Survey">
            3. Popularity Survey<a class="anchor-link" href="#3.-Popularity-Survey">¶</a>
          </h1>
          
          <h2 id="3-1.-user-information-from-official-account">
            3-1. user information from official account<a class="anchor-link" href="#3-1.-user-information-from-official-account">¶</a>
          </h2>
          
          <p>
            One way we can get an easy measurement of if a game is popular or not is to pull out some information associated with its official twitter account, such as the number of followers and number of likes. Normally, a more popular game would be garnished with more followers and more likes. However, cautions are needed as not every twitter user who plays a particular game would follow its official account on twitter.
          </p>
          
          <p>
            The following plot shows total number of followers to-date of a list of 14 popular mobile games (list based on internet reviews in 2015 and 2016):
          </p>
          
          <ul>
            <li>
              There are <strong>two winners: Clash of Clans and Pokemon Go</strong>, both have followers more than 2 millions, which clearly shows both are or were very popular games (follower number only goes up with time, so there is a bias toward games with longer time spans.)
            </li>
          </ul>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [204]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython2">
              <pre><span class="kn">import</span> <span class="nn">pylab</span>
<span class="n">pylab</span><span class="o">.</span><span class="n">rcParams</span><span class="p">[</span><span class="s1">'figure.figsize'</span><span class="p">]</span> <span class="o">=</span> <span class="p">[</span><span class="mi">10</span><span class="p">,</span><span class="mi">5</span><span class="p">]</span>
<span class="n">df_gl</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="s1">'data/pop1.csv'</span><span class="p">,</span><span class="n">sep</span><span class="o">=</span><span class="s1">'</span><span class="se">\t</span><span class="s1">'</span><span class="p">,</span><span class="n">index_col</span><span class="o">=</span><span class="mi"></span><span class="p">)</span>
<span class="n">current_time</span> <span class="o">=</span> <span class="s1">'2016-10-29 00:00:00'</span>
<span class="n">df_gl</span><span class="p">[</span><span class="s1">'days'</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="n">pd</span><span class="o">.</span><span class="n">datetime</span><span class="o">.</span><span class="n">now</span><span class="p">()</span><span class="o">.</span><span class="n">date</span><span class="p">()</span> <span class="o">-</span> <span class="n">pd</span><span class="o">.</span><span class="n">to_datetime</span><span class="p">(</span><span class="n">df_gl</span><span class="p">[</span><span class="s1">'created'</span><span class="p">]))</span><span class="o">.</span><span class="n">apply</span><span class="p">(</span><span class="k">lambda</span> <span class="n">x</span><span class="p">:</span> <span class="n">x</span> <span class="o">/</span> <span class="n">np</span><span class="o">.</span><span class="n">timedelta64</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span><span class="s1">'D'</span><span class="p">))</span>
<span class="n">df_gl</span><span class="o">.</span><span class="n">plot</span><span class="o">.</span><span class="n">bar</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="n">df_gl</span><span class="o">.</span><span class="n">index</span><span class="p">,</span><span class="n">y</span><span class="o">=</span><span class="s1">'followers'</span><span class="p">,</span><span class="n">rot</span><span class="o">=</span><span class="mi">80</span><span class="p">)</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt output_prompt">
              Out[204]:
            </div>
            
            <div class="output_text output_subarea output_execute_result">
              <pre>&lt;matplotlib.axes._subplots.AxesSubplot at 0x2ad13ef4cdd0&gt;</pre>
            </div>
          </div>
          
          <div class="output_area">
            <div class="prompt">
            </div>
            
            <div class="output_png output_subarea ">
              <img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAn4AAAGlCAYAAABkwfsRAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAALEgAACxIB0t1+/AAAIABJREFUeJzs3XucXfO9//HXJxchEUmRZEpJxP2uCEXIJKQUp8cpGi2qbq1LK02VU3pBOa1LS13rcn4nLqVabbWoIsWgoiQu1TZtESFIMhFEyE0un98fn+/KrGx7kpGZ2Wsy6/18POYxs/f67LW+s/bea33W97bM3RERERGRzq9L0QUQERERkdpQ4iciIiJSEkr8REREREpCiZ+IiIhISSjxExERESkJJX4iIiIiJdFtZQFmdjBwMrAGsDbwDvDf7v63XMw5wCFpGYAB89z9oIp1nQ0cCiwE3gBOcfc3c8u7ARcD+wBLgeeAb7j7vFxMb+AKYFsicf0TcLa7L83F1AHXAv1TuX/h7j+pKMtWwNVAd2At4HJ3//nK9oeIiIjI6qolNX5jgZvdfaS77wH8FXjQzPpVxI129xHpZ3iVpO804EhgqLvvCbwC3FmxjouBHYEh7r4b0Be4oSLmJqBLWr4HsDdwfm47BtwNPJe2MwI42cxOyMX0Au4HbnH3fYik9XIzG9mC/SEiIiKyWmpJ4veIu/8y9/gnwPrAp1u6kZSMnQ1c7e7z09OXAHua2fAU0xc4FfiJN80qfQnwBTMbnGK2I5K0iwDcfRHwU2C0mfVMrzmISB4vTTFzgOuA7+aKdCywprvfmGLeAG6viBERERHpVFaa+Ln7YRVPZYlbj4+wnR2IZtenc+udCUwFslq2eqLp+enc654FlgD7pcf7AfPdfVIuZgLQExiaHu8LTE4JXz5mIzPbIhfzTEUZJxCJ6Jof4f8SERERWW2syuCOPYnk766K5483s4fN7DEzu8nMNs8tGww4ML3iNTPSMoBNAHf3xmyhuy8G3qqIaWR5M3LbyH5X2461IKYLMAgRERGRTmhVEr/vAt9x91m556YSAzH2dfe9gX8CT5vZwLS8V/q9sGJdC4nauixmUZXtVcZUWwftECMiIiLSqax0VG+emf0IeMXdf5p/3t3HVjy+0MxOAkYD3wTmpkWVzcM9gGzE7lxihG2lyphq66AipncLYla2nmXMzCufExEREemo3N2qPd/iGj8z+wawFTEwoiWmAJulv18mmlrrKmLqgMn5GDPrn9tmV2A94KVcTH+Wl60zH1NtO16xrWoxS4nRxh/i7m32c84557Tp+tr6R+VT+VS+1a9sKp/KV/SPytdxyrYiLUr80lQoBwCfd/elZraJme2bW/7TKi/bkGgCBnie6Ju3a+41/YGNgXHpqUeAD/IxwM6pjA+mx+OAtcxsm1zMEKKWbnwuZjMzW6ci5jV3fzEXs3NFeYcA4919QZX/RURERGS1t9LEz8yOIKZi+R9gBzPbhRiJu1cu7LNpoufsNUcBA4HrIUZsAD8ETslNu/It4HF3b0gxs4kJlceYWdc0BczpwG3uPiXFTCLm/jsjbac7cBpwmTdN8vxHor/hmBSzDnAiubn+iLkAF5jZMSlmQ2BURYyIiIhIp9KSPn43A12Bhornz8v9fTbwDTP7JtFXbhEw0t2fzwLc/UozWxv4s5ktAKYB/1WxzrOAC4Enabpzx+iKmC8DV5rZU0TiOg44J7cdN7PPAteZ2fhUnmvd/f/lYuaa2aeBa83seGJAx2h3/1ML9ker1dfX12Izq0zlax2Vr3U6cvk6ctlA5Wstla91VL5VV8uy2cragiUGd2g/iYiIyOrAzPBmBnd8pFG9IiIiUm6DBg3i1VdfLboYAgwcOJBXXnnlI71GNX4toBo/ERGRkGqTii6G0Px7saIav1WZwFlEREREVkNK/ERERERKQomfiIiISEko8RMREREpCSV+IiIi0mnMmzePgw8+mL322oudd96Z1157rWrcoYceylprrcWjjz7KokWLGD58OF26dGHq1KlV4zsLTeciIiIirVJXN4jGxvab4mXAgIHMmPFKi2Jvv/12Fi9ezOOPP869995Lly7V67h+85vfMHjwYAC6d+/Oww8/TNeuXduqyB2WEj8RERFplUj62m+Kl8bGqjOTVPX666+zwQYbAHDggQeuMLZyKpQyTFOjpl4RERHpFG644QbGjh3Lfffdx4gRI3jsscf48Y9/zB577ME+++zDCSecwNy5c1u8vksuuWTZa48//njmzp3L3Llz2X777enTpw+jR49ett0jjjgCgHvvvZdBgwZx+OGHAzB58mT2339/6uvrGTZsGE888QQAd999N1tvvTX19fWceeaZ7LHHHmy66abMnz+fUaNGMXz4cPbZZx+++c1vtu1Ocnf9rOQndpOIiIhUOycCDt6OPy0/D5977rl+7LHHurv7Lbfc4tttt50vWLDA3d1POOEEP/7445fFDho0yB955JFlj83MX331VXd3v/nmm5t97UsvveR9+vTxxYsXu7v7YYcd5uuuu64vXbrU3d2PPvpoX7p0qS9evNi33nprv/HGG93d/fnnn/f111/f33//fXd3v/HGG71Xr17+wgsvuLv7mWee6ddcc42fcsop7u6+dOlS32233T7Se5F7vmpOoxo/ERER6ZRuvvlmRo0aRY8ePQA49thj+fnPf96iJt1bbrml2dduuummfPzjH6ehoYFFixbRs2dP1lprLcaPH8/8+fNZY401MDP+8pe/8PLLL3PUUUcBsP3227Phhhtyzz33LNvOlltuyeabbw7ARRddxLrrrstjjz3GU089hZnxyCOPtOk+UR8/ERER6ZRef/11+vXrt+xxv379WLRoEY2NjdTV1bXqtQcddBB333037s7w4cPp0aMH99xzD2+//TYjRowA4I033gBg5MiRQLSyfvDBB7z77rvL1tunT5/ltjtq1CiWLFnC6NGjefvttxkzZgwnnXRS63ZEjhI/ERER6ZQ22mgj3nzzzWWPZ86cSffu3RkwYECzrzGzFr324IMP5sQTT6R79+6ceeaZ9O3bl3POOYc5c+ZwwQUXLFvHGmuswUMPPbRsPfPmzVvh6OG33nqLUaNG8cUvfpG//vWv7Lvvvmy99dYMGzZs1XZCBTX1ioiISKf05S9/mV/96lcsXLgQiKbfL33pS8uSu2qyZuCVvXbo0KHMmjWLf/zjH/Tr14+RI0fywgsv8Prrr/Oxj30MgN13352NN96YO++8E4DFixdzyCGH8MILLyy3rbyrrrpqWVPwtttuy3rrrceSJUvaYncAqvETERGRVhowYOBHmnJlVdbfEjfccAM33XQTCxYsYOTIkYwbN45p06YxfPhwunXrxhZbbMHll18OxATOjY2NfOMb3+C6667jzDPPxMw44ogj+M1vfsMXvvAFpk+fXvW1AN26dWP//fdnu+22A6BXr14MGzaMvfbaa1lMly5duPvuuznllFO44oorWLp0Kccddxzbb789Dz/8MBdddBGNjY0ccMAB3HfffQAccMABfP/73+fqq69m9uzZHH744cuajtuCtaSDY9mZmWs/iYiIRFOozokdQ3PvRXq+aiaupl4RERGRklDiJyIiIlISSvxERERESkKJn4iIiEhJKPETERERKQklfiJS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QUVM7xbErGw9yzn33HOX/V1fX099fX21MBEREZGaamhooKGhoUWxbZH4TUm/6yqerwMmp79fJpLDOqJfXz7mwXyMmfVP/f8ws67AesBLuZj+VbZDRcz+VWK8ojzVyruUGG38IfnET0RERKSjqKyQOu+885qNbXVTr7vPBiYCu2bPpVG9OwLj0lPPE33z8jH9gY1zMY8AH+RjgJ1TGbPkcBywVhplnBlC1NKNz8VsZmbrVMS85u4v5mJ2rvhXhgDj3X3Byv9rERERkdXPR038LP1UugA4Ojch81eI6VxugxixAfwQOCU3IfO3gMfdvSHFzAauBsaYWdc0BczpwG3uPiXFTCLm/jsDYlJp4DTgMnfPmmj/SIwoHpNi1gFOJDfXHzEX4AIzOybFbAiMqogRERER6VRaOo9fd+ABoA9Rk/ckMM3dD8vFHAecSvSfWwCcVDkFjJmdBRyelk9LMbMqtnMhMIxodn0OGO3u83MxawNXAtsSies44DvuvjQXUwdcB/Qj+u7d6u6XVpRlC+Baorm7J5E83trM/695/ERaSXOVdV56b1tH+0/a2orm8WtR4ld2SvxEWk8nt85L723raP9JW2v1BM4iIiIisvpT4iciIiJSEkr8REREREpCiZ+IiIhISSjxExERESkJJX4iIiIiJaHET0RERKQklPiJiIiIlIQSPxEREZGSUOInIiIiUhJK/ERERERKQomfiIiISEko8RMREREpCSV+IiIiIiWhxE9ERESkJJT4iYiIiJSEEj8RERGRklDiJyIiIlISSvxERERESkKJn4iIiEhJKPETERERKQklfiIiIiIlocRPREREpCSU+ImIiIiUhBI/ERERkZJQ4iciIiJSEkr8REREREpCiZ+IiIhISSjxExERESkJJX4iIiIiJaHET0RERKQklPiJiIiIlIQSvxKpqxuEmbXZT13doKL/JREREfkIzN2LLkOHZ2beGfaTmQFt+X8YnWG/SG3o89d56b1tHe2/1qmrG0Rj46tttr4BAwYyY8Yrbba+IpgZ7m5Vl5Xpw7GqlPg1u8ZSHVykdfT567z03raO9l/raP992IoSPzX1ioiIiJSEEj8RERGRklDiJyIiIlISSvxERERESkKJn4iIiEhJKPETERERKQklfiIiIiIlocRPREREpCTaJPEzs2PM7J9m9lD6eTj97p2LOcHMJprZo2Z2v5kNrrKes83saTMbb2Z3mFm/iuXdzOzStJ6nzOx6M+tZEdPbzMam5RPN7EIz61IRU2dmv0vbmWhmp7fFfhARERHpyNqyxu9H7j4i/QxPv98DMLP/BC4APuPu+wB3AQ+Y2RrZi83sNOBIYKi77wm8AtxZsY2LgR2BIe6+G9AXuKEi5iagS1q+B7A3cH5uOwbcDTyXtjMCONnMTmiTvSAiIiLSQdWqqfe7wM3u/mZ6fB2wPpHoZcnY2cDV7j4/xVwC7Glmw1NMX+BU4Ce5+6ddAnwhqz00s+2AQ4CLANx9EfBTYHSuZvAgInm8NMXMSeX5bjv83yIiIiIdRrsnfilh2wV4OnvO3RcDzwEj01M7Av0rYmYCU3Mx9UC3fAzwLLAE2C893g+Y7+6TcjETgJ7A0PR4X2BySvjyMRuZ2Rar9E+KiIiIrAbaMvH7DzN7MPXh+5WZ7Zqe3yT9nl4RPwMYnIvxlsS4e2O2MCWQb1XENLK8Gen34NzvatuxXIyIiIhIp9NWiV8j8CJNffh+BzxhZrsBvYikbmHFaxYSNXGkGFoQs6jKtitjqq2DjxgjIiIi0um0SeLn7ve5+9nu/kF6fBvwBPBtYC5Rm9aj4mU9gHnp77m551YU073K5itjqq2DjxgjIiIi0ul0a8d1Tyb69k1Jj+sqltelGICXieSwjujXl495MB9jZv1T/z/MrCuwHvBSLqZ/le1QEbN/lRjPledDzj333GV/19fXU19f31yoiIiISM00NDTQ0NDQolhrGiC76szsh8AP3H1B7rkHgIXu/h9m9hTQ4O5npmXdgDeBMe5+YxrVOw04392vSTH9ib53I9y9IQ0SmQ4c6u73ppghwF+Azdx9ipltA/wN2D4b4GFmhwNjgf7uPs/MDiSaotfPBniY2RnAqe4+qJn/z9tiPxUtdnNb/h9GZ9gvUhv6/HVeem9bR/uvdbT/PszMcHertqyt+vjtARyf2+AwYDhwTXrqAuDo3ITMXwFmAbdBjNgAfgickpt25VvA4+7ekGJmA1cDY8ysa0oWTwduc/cpKWYSMfffGakc3YHTgMvcPWvG/SMxonhMilkHOJHcXH8iIiIinVFb1fh9Gvg60Bvomn4ucfc7czHHEfPwzQUWACe5+8sV6zkLODwtn5ZiZuWWdwcuBIYBS4kEbnRu7j/MbG3gSmBbIrEdB3zH3ZfmYuqIufv6Ef37bnX3S1fw/6nGr/oaV/urIqkdff46L723raP91zrafx+2ohq/Nkn8Ojslfs2ucbX/ckjt6PPXeem9bR3tv9bR/vuwWjT1ioiIiEgHp8RPREREpCSU+ImIiIiUhBI/ERERkZJQ4iciIiJSEkr8REREREpCiZ+IiIhISSjxExERESkJJX4iIiIiJaHET0RERKQklPiJiIiIlIQSPxEREZGSUOJIlfEUAAAgAElEQVQnIiIiUhJK/ERERERKQomfiIiISEko8RMREREpCSV+IiIiIiWhxE9ERESkJJT4iYiIiJSEEj8RERGRklDiJyIiIlISSvxERERESkKJn4iIiEhJKPETERERKQklfiIiIiIlocRPREREpCSU+ImIiIiUhBI/ERERkZJQ4iciIiJSEkr8REREREpCiZ+IiIhISSjxExERESkJJX4iUnp1dYMwszb7qasbVPS/JCJSlRI/kU5Cycuqa2x8FfA2+4n1SUeh74ZIE3P3osvQ4ZmZd4b9ZGbEianN1khn2C+dRUd/fzty+Tpy2VYHHX3/qXydm/bfh5kZ7m7VlqnGT0RERKQddMTaZtX4tYBq/Jpd42p/VdSZdPT3tyOXryOXbXXQ0fefyte5deT9V1TZVOMnIiIiIkr8RERERMpCiZ+IiIhISSjxExERESkJJX4iIh1cRxwZKCKrJ43qbQGN6m12jaUaOdbRdfT3tyOXryOXDVS+Vq9N5evUOvL+06heERERESlMqRM/M/usmT1lZg1m9piZ7VJ0mURERETaS7eiC1CUlOTdCuzq7v82s4OA+81sG3efWXDxRERERNpcmWv8vg3c5+7/BnD3PwCNwKntveGGhob23kQrNRRdgBXq6Puvo5evo7+/Hbt8DUUXYCUaii7ASjQUXYCVaCi6ACvRUHQBVkjHvtZoqNmWypz47QdMrHhuAjCyvTesL0frdPT919HL19Hf345dvoaiC7ASDUUXYCUaii7ASjQUXYCVaCi6ACukY19rNNRsS6VM/MzsY0AfYHrFohnA4NqXSKDlU1acd955mrJCRERkFZQy8QN6pd8LK55fCPSscVkkaWx8lRj2vrKfc1oUF+trO0pMRaSMdOzrXEo5j1+q8XsL+LK735x7/sL0XF1FfPl2koiIiKy2mpvHr5Sjet39HTObDdRVLKoDJleJr7rzRERERFYn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" />
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <p>
            In order to show the bias, or extract a unbiased analysis, we here plot number of followers (left) and number of days of the game&#8217;s lifetime (right) together. Note Pokemon Go only released this June, but the official account was registered in 2014 which is when that game is conceived.
          </p>
          
          <ul>
            <li>
              Both <strong>Clash of Clans and Pokemon Go</strong> have a lifetime close or below the average ages of the list of games we considered. However their follower counts are exceptional, clearly indicate their popularity in recent years. Especially for Pokemon Go, it shows a strong momentum to keep its popularity.
            </li>
          </ul>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [163]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython2">
              <pre><span class="kn">import</span> <span class="nn">pylab</span>
<span class="n">pylab</span><span class="o">.</span><span class="n">rcParams</span><span class="p">[</span><span class="s1">'figure.figsize'</span><span class="p">]</span> <span class="o">=</span> <span class="p">[</span><span class="mi">10</span><span class="p">,</span><span class="mi">5</span><span class="p">]</span>

<span class="n">dftmp</span><span class="o">=</span><span class="n">df_gl</span><span class="o">.</span><span class="n">sort_values</span><span class="p">(</span><span class="s1">'followers'</span><span class="p">)</span>
<span class="n">ygl</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">arange</span><span class="p">(</span><span class="n">df_gl</span><span class="p">[</span><span class="s1">'likes'</span><span class="p">]</span><span class="o">.</span><span class="n">size</span><span class="p">)</span>

<span class="n">fig</span><span class="p">,</span> <span class="n">axes</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="n">ncols</span><span class="o">=</span><span class="mi">2</span><span class="p">,</span> <span class="n">sharey</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span>
<span class="n">axes</span><span class="p">[</span><span class="mi"></span><span class="p">]</span><span class="o">.</span><span class="n">barh</span><span class="p">(</span><span class="n">ygl</span><span class="p">,</span> <span class="n">dftmp</span><span class="p">[</span><span class="s1">'followers'</span><span class="p">]</span><span class="o">*</span><span class="mf">0.001</span><span class="p">,</span> <span class="n">align</span><span class="o">=</span><span class="s1">'center'</span><span class="p">,</span> <span class="n">color</span><span class="o">=</span><span class="s1">'blue'</span><span class="p">,</span> <span class="n">zorder</span><span class="o">=</span><span class="mi">10</span><span class="p">)</span>
<span class="n">axes</span><span class="p">[</span><span class="mi"></span><span class="p">]</span><span class="o">.</span><span class="n">set</span><span class="p">(</span><span class="n">title</span><span class="o">=</span><span class="s1">'Number of followers('</span><span class="o">+</span><span class="s1">r'$\times 1000$)'</span><span class="p">)</span>
<span class="n">axes</span><span class="p">[</span><span class="mi">1</span><span class="p">]</span><span class="o">.</span><span class="n">barh</span><span class="p">(</span><span class="n">ygl</span><span class="p">,</span> <span class="n">dftmp</span><span class="p">[</span><span class="s1">'days'</span><span class="p">],</span> <span class="n">align</span><span class="o">=</span><span class="s1">'center'</span><span class="p">,</span> <span class="n">color</span><span class="o">=</span><span class="s1">'red'</span><span class="p">,</span> <span class="n">zorder</span><span class="o">=</span><span class="mi">10</span><span class="p">)</span>
<span class="n">axes</span><span class="p">[</span><span class="mi">1</span><span class="p">]</span><span class="o">.</span><span class="n">set</span><span class="p">(</span><span class="n">title</span><span class="o">=</span><span class="s1">'Number of days'</span><span class="p">)</span>

<span class="n">axes</span><span class="p">[</span><span class="mi"></span><span class="p">]</span><span class="o">.</span><span class="n">invert_xaxis</span><span class="p">()</span>
<span class="n">axes</span><span class="p">[</span><span class="mi"></span><span class="p">]</span><span class="o">.</span><span class="n">set</span><span class="p">(</span><span class="n">yticks</span><span class="o">=</span><span class="n">ygl</span><span class="p">,</span> <span class="n">yticklabels</span><span class="o">=</span><span class="n">dftmp</span><span class="o">.</span><span class="n">index</span><span class="p">)</span>
<span class="n">axes</span><span class="p">[</span><span class="mi"></span><span class="p">]</span><span class="o">.</span><span class="n">yaxis</span><span class="o">.</span><span class="n">tick_right</span><span class="p">()</span>

<span class="k">for</span> <span class="n">ax</span> <span class="ow">in</span> <span class="n">axes</span><span class="o">.</span><span class="n">flat</span><span class="p">:</span>
    <span class="n">ax</span><span class="o">.</span><span class="n">margins</span><span class="p">(</span><span class="mf">0.01</span><span class="p">)</span>
    <span class="n">ax</span><span class="o">.</span><span class="n">grid</span><span class="p">(</span><span class="bp">True</span><span class="p">)</span>

<span class="n">fig</span><span class="o">.</span><span class="n">tight_layout</span><span class="p">()</span>
<span class="n">fig</span><span class="o">.</span><span class="n">subplots_adjust</span><span class="p">(</span><span class="n">wspace</span><span class="o">=</span><span class="mf">0.4</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt">
            </div>
            
            <div class="output_png output_subarea ">
              <img src="data:image/png;base64,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" />
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <p>
            On the other hand, number of likes might not be a good indicator of a game&#8217;s recent popularity. Some games gained more likes due to their longevity, such as angry birds and Plants vs Zombies. Some popular games such as Pokemon Go gains less likes partly because of its very young age. One exception is Ingress, a location based, multiplayer online game, a relative of Pokemon Go. It attracts the third highest number of likes within a time span less than the averaged lifetime of the games in the list.
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [161]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython2">
              <pre><span class="n">dftmp</span><span class="o">=</span><span class="n">df_gl</span><span class="o">.</span><span class="n">sort_values</span><span class="p">(</span><span class="s1">'days'</span><span class="p">)</span>
<span class="n">ygl</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">arange</span><span class="p">(</span><span class="n">df_gl</span><span class="p">[</span><span class="s1">'likes'</span><span class="p">]</span><span class="o">.</span><span class="n">size</span><span class="p">)</span>

<span class="n">fig</span><span class="p">,</span> <span class="n">axes</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="n">ncols</span><span class="o">=</span><span class="mi">2</span><span class="p">,</span> <span class="n">sharey</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span>
<span class="n">axes</span><span class="p">[</span><span class="mi"></span><span class="p">]</span><span class="o">.</span><span class="n">barh</span><span class="p">(</span><span class="n">ygl</span><span class="p">,</span> <span class="n">dftmp</span><span class="p">[</span><span class="s1">'likes'</span><span class="p">],</span> <span class="n">align</span><span class="o">=</span><span class="s1">'center'</span><span class="p">,</span> <span class="n">color</span><span class="o">=</span><span class="s1">'blue'</span><span class="p">,</span> <span class="n">zorder</span><span class="o">=</span><span class="mi">10</span><span class="p">)</span>
<span class="n">axes</span><span class="p">[</span><span class="mi"></span><span class="p">]</span><span class="o">.</span><span class="n">set</span><span class="p">(</span><span class="n">title</span><span class="o">=</span><span class="s1">'Number of likes'</span><span class="p">)</span>
<span class="n">axes</span><span class="p">[</span><span class="mi">1</span><span class="p">]</span><span class="o">.</span><span class="n">barh</span><span class="p">(</span><span class="n">ygl</span><span class="p">,</span> <span class="n">dftmp</span><span class="p">[</span><span class="s1">'days'</span><span class="p">],</span> <span class="n">align</span><span class="o">=</span><span class="s1">'center'</span><span class="p">,</span> <span class="n">color</span><span class="o">=</span><span class="s1">'red'</span><span class="p">,</span> <span class="n">zorder</span><span class="o">=</span><span class="mi">10</span><span class="p">)</span>
<span class="n">axes</span><span class="p">[</span><span class="mi">1</span><span class="p">]</span><span class="o">.</span><span class="n">set</span><span class="p">(</span><span class="n">title</span><span class="o">=</span><span class="s1">'Number of days'</span><span class="p">)</span>

<span class="n">axes</span><span class="p">[</span><span class="mi"></span><span class="p">]</span><span class="o">.</span><span class="n">invert_xaxis</span><span class="p">()</span>
<span class="n">axes</span><span class="p">[</span><span class="mi"></span><span class="p">]</span><span class="o">.</span><span class="n">set</span><span class="p">(</span><span class="n">yticks</span><span class="o">=</span><span class="n">ygl</span><span class="p">,</span> <span class="n">yticklabels</span><span class="o">=</span><span class="n">dftmp</span><span class="o">.</span><span class="n">index</span><span class="p">)</span>
<span class="n">axes</span><span class="p">[</span><span class="mi"></span><span class="p">]</span><span class="o">.</span><span class="n">yaxis</span><span class="o">.</span><span class="n">tick_right</span><span class="p">()</span>

<span class="k">for</span> <span class="n">ax</span> <span class="ow">in</span> <span class="n">axes</span><span class="o">.</span><span class="n">flat</span><span class="p">:</span>
    <span class="n">ax</span><span class="o">.</span><span class="n">margins</span><span class="p">(</span><span class="mf">0.01</span><span class="p">)</span>
    <span class="n">ax</span><span class="o">.</span><span class="n">grid</span><span class="p">(</span><span class="bp">True</span><span class="p">)</span>

<span class="n">fig</span><span class="o">.</span><span class="n">tight_layout</span><span class="p">()</span>
<span class="n">fig</span><span class="o">.</span><span class="n">subplots_adjust</span><span class="p">(</span><span class="n">wspace</span><span class="o">=</span><span class="mf">0.4</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt">
            </div>
            
            <div class="output_png output_subarea ">
              <img src="data:image/png;base64,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" />
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <h2 id="2.2-tweets-count">
            2.2 tweets count<a class="anchor-link" href="#2.2-tweets-count">¶</a>
          </h2>
          
          <p>
            Another way to measure the popularity of a game is by counting how many times twitter users mentioned the game. I therefore scrapped the tweets on the web within the past week for the following six games: Candy Crush, Clash of Clans, Flappy Bird, Plants vs Zombies, Subway Surfers, Pokemon Go. The reason I choose those games is partly because my kids and wife like to play them, and so do I.
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [ ]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython2">
              <pre><span class="kn">import</span> <span class="nn">glob</span>
<span class="kn">import</span> <span class="nn">pandas</span> <span class="kn">as</span> <span class="nn">pd</span>
<span class="kn">import</span> <span class="nn">numpy</span> <span class="kn">as</span> <span class="nn">np</span>
<span class="kn">import</span> <span class="nn">scipy</span>
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="kn">as</span> <span class="nn">plt</span>
<span class="kn">import</span> <span class="nn">random</span>
<span class="kn">import</span> <span class="nn">os</span>

<span class="k">def</span> <span class="nf">merge_files</span><span class="p">(</span><span class="n">filenames</span><span class="p">,</span><span class="n">outfilename</span><span class="p">):</span>
  <span class="n">first_time</span> <span class="o">=</span> <span class="bp">True</span>
  <span class="k">for</span> <span class="nb">file</span> <span class="ow">in</span> <span class="n">filenames</span><span class="p">:</span>
    <span class="k">if</span> <span class="n">os</span><span class="o">.</span><span class="n">stat</span><span class="p">(</span><span class="nb">file</span><span class="p">)</span><span class="o">.</span><span class="n">st_size</span> <span class="o">==</span> <span class="mi"></span><span class="p">:</span>
      <span class="k">continue</span>
    <span class="k">if</span> <span class="n">first_time</span><span class="p">:</span> 
      <span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="nb">file</span><span class="p">,</span><span class="n">index_col</span><span class="o">=</span><span class="bp">None</span><span class="p">,</span><span class="n">header</span><span class="o">=</span><span class="bp">None</span><span class="p">,</span><span class="n">sep</span><span class="o">=</span><span class="s1">'</span><span class="se">\t</span><span class="s1">'</span><span class="p">)</span>
      <span class="n">first_time</span><span class="o">=</span><span class="bp">False</span>
    <span class="k">else</span><span class="p">:</span>
      <span class="k">print</span> <span class="nb">file</span>
      <span class="n">tmp</span><span class="o">=</span><span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="nb">file</span><span class="p">,</span><span class="n">index_col</span><span class="o">=</span><span class="bp">None</span><span class="p">,</span> <span class="n">header</span><span class="o">=</span><span class="bp">None</span><span class="p">,</span><span class="n">sep</span><span class="o">=</span><span class="s1">'</span><span class="se">\t</span><span class="s1">'</span><span class="p">)</span>
      <span class="n">df</span><span class="o">=</span><span class="n">df</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">tmp</span><span class="p">,</span><span class="n">ignore_index</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span>
        
  <span class="n">df</span><span class="o">.</span><span class="n">to_csv</span><span class="p">(</span><span class="n">outfilename</span><span class="p">,</span><span class="n">sep</span><span class="o">=</span><span class="s1">'</span><span class="se">\t</span><span class="s1">'</span><span class="p">)</span>
  <span class="k">print</span> <span class="s1">'there are total tweets = '</span><span class="p">,</span> <span class="n">df</span><span class="p">[</span><span class="mi"></span><span class="p">]</span><span class="o">.</span><span class="n">count</span><span class="p">()</span>


<span class="n">games</span> <span class="o">=</span> <span class="p">[</span><span class="s1">'ClashofClans'</span><span class="p">,</span><span class="s1">'FlappyBird'</span><span class="p">,</span><span class="s1">'PvZ2'</span><span class="p">,</span><span class="s1">'SubwaySurfer'</span><span class="p">,</span><span class="s1">'CandyCrush'</span><span class="p">,</span><span class="s1">'PokemonGo'</span><span class="p">]</span>

<span class="k">for</span> <span class="n">name</span> <span class="ow">in</span> <span class="n">games</span><span class="p">:</span>
  <span class="n">filenames</span> <span class="o">=</span> <span class="n">glob</span><span class="o">.</span><span class="n">glob</span><span class="p">(</span><span class="s2">"data/"</span><span class="o">+</span><span class="n">name</span><span class="o">+</span><span class="s2">"/*.csv"</span><span class="p">)</span>
  <span class="n">output</span> <span class="o">=</span> <span class="s1">'data/'</span><span class="o">+</span><span class="n">name</span><span class="o">+</span><span class="s1">'.csv'</span>
  <span class="k">print</span> <span class="s1">'in '</span><span class="p">,</span><span class="n">output</span><span class="p">,</span><span class="s1">':'</span>
  <span class="n">merge_files</span><span class="p">(</span><span class="n">filenames</span><span class="p">,</span><span class="n">output</span><span class="p">)</span>
</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <p>
            The following plot shows the number of tweets that mentioned individual game in the past week.
          </p>
          
          <ul>
            <li>
              It is not surprising to see Pokemon Go alone hits 70K tweets,while the rest of five combined only gives 10K.
            </li>
          </ul>
          
          <p>
            It indicates that,
          </p>
          
          <ul>
            <li>
              1) overall Pokemon Go is the most dominant mobile game based on social media , or
            </li>
            <li>
              2) Pokemon Go players tweet much more often (almost 100 times) than other game players do
            </li>
          </ul>
          
          <p>
            although the second might not be so likely. Further study with data over longer time span, and/or get user information might be very useful to tell. <strong>In any rate, Pokemon Go does a great job to get its players excited indicated by the huge amount of tweets over a relatively short period of time.</strong>
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [12]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython2">
              <pre><span class="kn">import</span> <span class="nn">numpy</span> <span class="kn">as</span> <span class="nn">np</span>
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="kn">as</span> <span class="nn">plt</span>
<span class="o">%</span><span class="k">matplotlib</span> inline

<span class="n">nbin</span> <span class="o">=</span> <span class="mi">2</span>
<span class="n">pokemon</span> <span class="o">=</span> <span class="p">[</span><span class="mi">72486</span><span class="p">,</span><span class="mi"></span><span class="p">]</span>
<span class="n">flappy</span> <span class="o">=</span><span class="p">[</span><span class="mi"></span><span class="p">,</span><span class="mi">2524</span><span class="p">]</span>
<span class="n">pvz2</span><span class="o">=</span><span class="p">[</span><span class="mi"></span><span class="p">,</span><span class="mi">6810</span><span class="p">]</span>
<span class="n">subway</span><span class="o">=</span><span class="p">[</span><span class="mi"></span><span class="p">,</span><span class="mi">1675</span><span class="p">]</span>
<span class="n">candy</span><span class="o">=</span><span class="p">[</span><span class="mi"></span><span class="p">,</span><span class="mi">1164</span><span class="p">]</span>
<span class="n">clash</span><span class="o">=</span><span class="p">[</span><span class="mi"></span><span class="p">,</span><span class="mi">6640</span><span class="p">]</span>

<span class="kn">import</span> <span class="nn">pylab</span>
<span class="n">pylab</span><span class="o">.</span><span class="n">rcParams</span><span class="p">[</span><span class="s1">'figure.figsize'</span><span class="p">]</span> <span class="o">=</span> <span class="p">[</span><span class="mi">4</span><span class="p">,</span><span class="mi">6</span><span class="p">]</span>

<span class="n">ind</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">arange</span><span class="p">(</span><span class="n">nbin</span><span class="p">)</span>    <span class="c1"># the x locations for the groups</span>
<span class="n">width</span> <span class="o">=</span> <span class="mf">0.15</span>       <span class="c1"># the width of the bars: can also be len(x) sequence</span>

<span class="n">p1</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">bar</span><span class="p">(</span><span class="n">ind</span><span class="p">,</span> <span class="n">pokemon</span><span class="p">,</span> <span class="n">width</span><span class="p">,</span> <span class="n">color</span><span class="o">=</span><span class="s1">'r'</span><span class="p">,</span><span class="n">align</span><span class="o">=</span><span class="s1">'center'</span><span class="p">)</span>
<span class="n">p2</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">bar</span><span class="p">(</span><span class="n">ind</span><span class="p">,</span> <span class="n">flappy</span><span class="p">,</span> <span class="n">width</span><span class="p">,</span> <span class="n">color</span><span class="o">=</span><span class="s1">'y'</span><span class="p">,</span>
             <span class="n">bottom</span><span class="o">=</span><span class="n">pokemon</span><span class="p">)</span>
<span class="n">p3</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">bar</span><span class="p">(</span><span class="n">ind</span><span class="p">,</span> <span class="n">pvz2</span><span class="p">,</span> <span class="n">width</span><span class="p">,</span> <span class="n">color</span><span class="o">=</span><span class="s1">'b'</span><span class="p">,</span>
             <span class="n">bottom</span><span class="o">=</span><span class="n">flappy</span><span class="p">)</span>
<span class="n">p4</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">bar</span><span class="p">(</span><span class="n">ind</span><span class="p">,</span> <span class="n">subway</span><span class="p">,</span> <span class="n">width</span><span class="p">,</span> <span class="n">color</span><span class="o">=</span><span class="s1">'g'</span><span class="p">,</span>
             <span class="n">bottom</span><span class="o">=</span><span class="n">flappy</span><span class="p">)</span>
<span class="n">p5</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">bar</span><span class="p">(</span><span class="n">ind</span><span class="p">,</span> <span class="n">candy</span><span class="p">,</span> <span class="n">width</span><span class="p">,</span> <span class="n">color</span><span class="o">=</span><span class="s1">'brown'</span><span class="p">,</span>
             <span class="n">bottom</span><span class="o">=</span><span class="n">pvz2</span><span class="p">)</span>
<span class="n">p6</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">bar</span><span class="p">(</span><span class="n">ind</span><span class="p">,</span> <span class="n">clash</span><span class="p">,</span> <span class="n">width</span><span class="p">,</span> <span class="n">color</span><span class="o">=</span><span class="s1">'cyan'</span><span class="p">,</span>
             <span class="n">bottom</span><span class="o">=</span><span class="n">candy</span><span class="p">)</span>

<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">'Total # of tweets (in one week)'</span><span class="p">,</span><span class="n">fontsize</span><span class="o">=</span><span class="mi">15</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xticks</span><span class="p">(</span><span class="n">ind</span> <span class="o">+</span> <span class="n">width</span><span class="o">/</span><span class="mf">2.</span><span class="p">,</span> <span class="p">(</span><span class="s1">'PokemonGo'</span><span class="p">,</span> <span class="s1">'Others'</span><span class="p">))</span>
<span class="c1">#plt.yticks(np.arange(0, 81, 10))</span>
<span class="n">plt</span><span class="o">.</span><span class="n">legend</span><span class="p">((</span><span class="n">p1</span><span class="p">[</span><span class="mi"></span><span class="p">],</span> <span class="n">p2</span><span class="p">[</span><span class="mi"></span><span class="p">],</span><span class="n">p3</span><span class="p">[</span><span class="mi"></span><span class="p">],</span><span class="n">p4</span><span class="p">[</span><span class="mi"></span><span class="p">],</span><span class="n">p5</span><span class="p">[</span><span class="mi"></span><span class="p">],</span><span class="n">p6</span><span class="p">[</span><span class="mi"></span><span class="p">]),</span> <span class="p">[</span><span class="s1">'PokemonGo'</span><span class="p">,</span><span class="s1">'FlappyBird'</span><span class="p">,</span><span class="s1">'PvZ2'</span><span class="p">,</span><span class="s1">'SubwaySurfer'</span><span class="p">,</span><span class="s1">'CandyCrush'</span><span class="p">,</span><span class="s1">'ClashofClans'</span><span class="p">])</span>

<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt">
            </div>
            
            <div class="output_png output_subarea ">
              <img class="size-medium wp-image-286 aligncenter" src="http://jimingshi.us/wp-content/uploads/2016/10/barchart-248x300.png" alt="barchart" width="248" height="300" srcset="http://jimingshi.us/wp-content/uploads/2016/10/barchart-248x300.png 248w, http://jimingshi.us/wp-content/uploads/2016/10/barchart.png 309w" sizes="(max-width: 248px) 100vw, 248px" />
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <h1 id="3.-Pattern-of-usage">
            3. Pattern of usage<a class="anchor-link" href="#3.-Pattern-of-usage">¶</a>
          </h1>
          
          <h2 id="3-1.-weekly-pattern">
            3-1. weekly pattern<a class="anchor-link" href="#3-1.-weekly-pattern">¶</a>
          </h2>
          
          <p>
            Before we move on to the text content, lets do a histogram of total count grouped by days of week. For this and following study, I have doubled the data size which now spans over the past two weeks (120k tweets in total). Based on the following plot,
          </p>
          
          <ul>
            <li>
              there is a clear uprising trend from Monday to Thursday, and a sudden drop on Friday and then gradually climb up back during the weekend.
            </li>
          </ul>
          
          <p>
            Whether it is an indicator of people spend more time on Pokemon Go from Monday to Thursday, or people tend to tweet more during Mon to Thursday is unclear at this moment.
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [37]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython2">
              <pre><span class="kn">import</span> <span class="nn">glob</span>
<span class="kn">import</span> <span class="nn">pandas</span> <span class="kn">as</span> <span class="nn">pd</span>
<span class="kn">import</span> <span class="nn">numpy</span> <span class="kn">as</span> <span class="nn">np</span>
<span class="kn">import</span> <span class="nn">scipy</span>
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="kn">as</span> <span class="nn">plt</span>
<span class="o">%</span><span class="k">matplotlib</span> inline
<span class="kn">import</span> <span class="nn">random</span>
<span class="kn">import</span> <span class="nn">os</span>
<span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="s1">'data/PokemonGo_week.csv'</span><span class="p">,</span><span class="n">sep</span><span class="o">=</span><span class="s1">'</span><span class="se">\t</span><span class="s1">'</span><span class="p">,</span><span class="n">index_col</span><span class="o">=</span><span class="mi"></span><span class="p">)</span>
<span class="n">df</span><span class="o">.</span><span class="n">columns</span> <span class="o">=</span><span class="p">[</span><span class="s1">'userid'</span><span class="p">,</span><span class="s1">'tweetid'</span><span class="p">,</span><span class="s1">'time'</span><span class="p">,</span><span class="s1">'username'</span><span class="p">,</span><span class="s1">'text'</span><span class="p">]</span>
</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [38]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython2">
              <pre><span class="n">timestamp</span><span class="o">=</span><span class="p">[]</span>
<span class="n">falselist</span><span class="o">=</span><span class="p">[]</span>
<span class="n">count</span><span class="o">=</span><span class="mi"></span>
<span class="k">for</span> <span class="n">stamp</span> <span class="ow">in</span> <span class="n">df</span><span class="p">[</span><span class="s1">'time'</span><span class="p">]:</span>
       <span class="k">if</span> <span class="nb">type</span><span class="p">(</span><span class="n">stamp</span><span class="p">)</span> <span class="ow">is</span> <span class="nb">str</span><span class="p">:</span>
          <span class="n">line</span><span class="o">=</span><span class="n">stamp</span><span class="o">.</span><span class="n">split</span><span class="p">(</span><span class="s1">' '</span><span class="p">)</span>
          <span class="n">hr</span><span class="p">,</span><span class="nb">min</span> <span class="o">=</span> <span class="n">line</span><span class="p">[</span><span class="mi"></span><span class="p">]</span><span class="o">.</span><span class="n">split</span><span class="p">(</span><span class="s1">':'</span><span class="p">)</span>
          <span class="k">if</span><span class="p">(</span><span class="n">line</span><span class="p">[</span><span class="mi">1</span><span class="p">]</span><span class="o">==</span><span class="s1">'PM'</span> <span class="ow">and</span> <span class="nb">int</span><span class="p">(</span><span class="n">hr</span><span class="p">)</span><span class="o">&lt;</span><span class="mi">12</span><span class="p">):</span>
            <span class="n">hr</span><span class="o">=</span><span class="nb">str</span><span class="p">(</span><span class="nb">int</span><span class="p">(</span><span class="n">hr</span><span class="p">)</span><span class="o">+</span><span class="mi">12</span><span class="p">)</span>
          <span class="n">timestamp</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="s1">'2016-10-'</span><span class="o">+</span><span class="n">line</span><span class="p">[</span><span class="mi">3</span><span class="p">]</span><span class="o">+</span><span class="s1">' '</span><span class="o">+</span><span class="n">hr</span><span class="o">+</span><span class="s1">':'</span><span class="o">+</span><span class="nb">min</span><span class="o">+</span><span class="s1">':00'</span><span class="p">)</span>
       <span class="k">else</span><span class="p">:</span>
          <span class="n">falselist</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">count</span><span class="p">)</span>
       <span class="n">count</span><span class="o">+=</span><span class="mi">1</span>
    
<span class="n">df1</span><span class="o">=</span><span class="n">df</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="n">df</span><span class="o">.</span><span class="n">index</span><span class="p">[</span><span class="n">falselist</span><span class="p">])</span>
<span class="c1">#print df1['time'].size</span>
</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [ ]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython2">
              <pre><span class="k">print</span> <span class="n">df1</span><span class="p">[</span><span class="s1">'userid'</span><span class="p">]</span><span class="o">.</span><span class="n">size</span>
<span class="n">df1</span><span class="p">[</span><span class="s1">'timestamp'</span><span class="p">]</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">Series</span><span class="p">(</span><span class="n">timestamp</span><span class="p">,</span> <span class="n">index</span><span class="o">=</span><span class="n">df1</span><span class="o">.</span><span class="n">index</span><span class="p">)</span>
<span class="n">df1</span><span class="p">[</span><span class="s1">'dayofweek'</span><span class="p">]</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">to_datetime</span><span class="p">(</span><span class="n">df1</span><span class="p">[</span><span class="s1">'timestamp'</span><span class="p">])</span><span class="o">.</span><span class="n">apply</span><span class="p">(</span><span class="k">lambda</span> <span class="n">x</span><span class="p">:</span> <span class="n">x</span><span class="o">.</span><span class="n">weekday</span><span class="p">())</span>
<span class="c1">#df1['dayofweek']</span>
</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [35]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython2">
              <pre><span class="n">x</span><span class="o">=</span><span class="n">np</span><span class="o">.</span><span class="n">arange</span><span class="p">(</span><span class="mi">7</span><span class="p">)</span>
<span class="n">ax</span><span class="o">=</span><span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">()</span>
<span class="c1">#df1.hist(column='dayofweek',alpha=0.5,grid=True,bins=7,xlabel)</span>
<span class="n">df1</span><span class="o">.</span><span class="n">plot</span><span class="o">.</span><span class="n">hist</span><span class="p">(</span><span class="n">y</span><span class="o">=</span><span class="s1">'dayofweek'</span><span class="p">,</span><span class="n">alpha</span><span class="o">=</span><span class="mf">0.5</span><span class="p">,</span><span class="n">grid</span><span class="o">=</span><span class="bp">True</span><span class="p">,</span><span class="n">bins</span><span class="o">=</span><span class="mi">7</span><span class="p">,</span><span class="n">align</span><span class="o">=</span><span class="s1">'mid'</span><span class="p">,</span><span class="nb">range</span><span class="o">=</span><span class="p">[</span><span class="o">-</span><span class="mf">0.4</span><span class="p">,</span><span class="mf">6.4</span><span class="p">],</span><span class="n">label</span><span class="o">=</span><span class="s1">'Days of week'</span><span class="p">)</span>
<span class="n">ax</span><span class="o">.</span><span class="n">set_xlabel</span><span class="o">=</span><span class="p">[</span><span class="s1">'M'</span><span class="p">,</span><span class="s1">'T'</span><span class="p">,</span><span class="s1">'W'</span><span class="p">,</span><span class="s1">'Th'</span><span class="p">,</span><span class="s1">'F'</span><span class="p">,</span><span class="s1">'S'</span><span class="p">,</span><span class="s1">'Su'</span><span class="p">]</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt">
            </div>
            
            <div class="output_text output_subarea ">
              <pre>&lt;matplotlib.figure.Figure at 0x2ae143b08890&gt;</pre>
            </div>
          </div>
          
          <div class="output_area">
            <div class="prompt">
            </div>
            
            <div class="output_png output_subarea ">
              <img src="data:image/png;base64,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" />
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <h2 id="3-2.-daily-pattern">
            3-2. daily pattern<a class="anchor-link" href="#3-2.-daily-pattern">¶</a>
          </h2>
          
          <ul>
            <li>
              Most of the tweets occur between the day time from 6am to 4pm which is reasonable
            </li>
            <li>
              It peaks at the noon time, which is perhaps because people have more free time during lunch
            </li>
          </ul>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [63]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython2">
              <pre><span class="c1">#df1['hour'] </span>
<span class="n">hourlist</span> <span class="o">=</span> <span class="p">[</span> <span class="nb">int</span><span class="p">(</span><span class="n">item</span><span class="o">.</span><span class="n">split</span><span class="p">(</span><span class="s1">' '</span><span class="p">)[</span><span class="mi">1</span><span class="p">]</span><span class="o">.</span><span class="n">split</span><span class="p">(</span><span class="s1">':'</span><span class="p">)[</span><span class="mi"></span><span class="p">])</span> <span class="k">for</span> <span class="n">item</span> <span class="ow">in</span> <span class="n">df1</span><span class="p">[</span><span class="s1">'timestamp'</span><span class="p">]]</span>
<span class="n">df1</span><span class="p">[</span><span class="s1">'hour'</span><span class="p">]</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">Series</span><span class="p">(</span><span class="n">hourlist</span><span class="p">,</span> <span class="n">index</span><span class="o">=</span><span class="n">df1</span><span class="o">.</span><span class="n">index</span><span class="p">)</span>
</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [65]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython2">
              <pre><span class="n">x</span><span class="o">=</span><span class="n">np</span><span class="o">.</span><span class="n">arange</span><span class="p">(</span><span class="mi">24</span><span class="p">)</span>
<span class="n">ax</span><span class="o">=</span><span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">()</span>
<span class="c1">#df1.hist(column='dayofweek',alpha=0.5,grid=True,bins=7,xlabel)</span>
<span class="n">df1</span><span class="o">.</span><span class="n">plot</span><span class="o">.</span><span class="n">hist</span><span class="p">(</span><span class="n">y</span><span class="o">=</span><span class="s1">'hour'</span><span class="p">,</span><span class="n">alpha</span><span class="o">=</span><span class="mf">0.5</span><span class="p">,</span><span class="n">grid</span><span class="o">=</span><span class="bp">True</span><span class="p">,</span><span class="n">bins</span><span class="o">=</span><span class="mi">24</span><span class="p">,</span><span class="n">align</span><span class="o">=</span><span class="s1">'mid'</span><span class="p">,</span><span class="nb">range</span><span class="o">=</span><span class="p">[</span><span class="mi"></span><span class="p">,</span><span class="mf">24.5</span><span class="p">],</span><span class="n">label</span><span class="o">=</span><span class="s1">'Hour'</span><span class="p">)</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt output_prompt">
              Out[65]:
            </div>
            
            <div class="output_text output_subarea output_execute_result">
              <pre>&lt;matplotlib.axes._subplots.AxesSubplot at 0x2b8062839650&gt;</pre>
            </div>
          </div>
          
          <div class="output_area">
            <div class="prompt">
            </div>
            
            <div class="output_text output_subarea ">
              <pre>&lt;matplotlib.figure.Figure at 0x2b8062912150&gt;</pre>
            </div>
          </div>
          
          <div class="output_area">
            <div class="prompt">
            </div>
            
            <div class="output_png output_subarea ">
              <img src="data:image/png;base64,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" />
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <h1 id="4.-Text-analysis">
            4. Text analysis<a class="anchor-link" href="#4.-Text-analysis">¶</a>
          </h1>
          
          <h2 id="3-2.-daily-pattern">
            4-1. terms occurrence<a class="anchor-link" href="#4.1-Terms-occurence">¶</a>
          </h2>
          
          <p>
            By searching and sorting all meaningful single words in the text of tweets within the last two weeks, here are the first 10 most frequent words:<br /> *(&#8216;twitter&#8217;, 38406), (&#8216;pic&#8217;, 23536), (&#8216;halloween&#8217;, 10795), (&#8216;video&#8217;, 9545), (&#8216;new&#8217;, 8537), (&#8216;update&#8217;, 7604), (&#8216;liked&#8217;, 7068), (&#8216;event&#8217;, 6850), (&#8216;play&#8217;, 5300), (&#8216;get&#8217;, 4227)
          </p>
          
          <ul>
            <li>
              The words &#8216;pic&#8217; and &#8216;video&#8217; clearly show the popular media content of the tweets;
            </li>
            <li>
              &#8216;halloween&#8217;, &#8216;new&#8217;, and &#8216;update&#8217; are related to recent update of the App;
            </li>
            <li>
              &#8216;halloween&#8217; and &#8216;event&#8217; refer to the newly announced halloween event which aims to stimulate the players to play even in this cool weather.<img class="size-full wp-image-292 aligncenter" src="http://jimingshi.us/wp-content/uploads/2016/10/word_count-1.png" alt="word_count" width="1023" height="552" srcset="http://jimingshi.us/wp-content/uploads/2016/10/word_count-1.png 1023w, http://jimingshi.us/wp-content/uploads/2016/10/word_count-1-300x162.png 300w, http://jimingshi.us/wp-content/uploads/2016/10/word_count-1-768x414.png 768w" sizes="(max-width: 1023px) 100vw, 1023px" />
            </li>
          </ul>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [ ]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython2">
              <pre><span class="kn">from</span> <span class="nn">nltk.corpus</span> <span class="kn">import</span> <span class="n">stopwords</span>
<span class="kn">import</span> <span class="nn">string</span>
<span class="kn">import</span> <span class="nn">operator</span> 
<span class="kn">import</span> <span class="nn">json</span>
<span class="kn">from</span> <span class="nn">collections</span> <span class="kn">import</span> <span class="n">Counter</span>
<span class="kn">import</span> <span class="nn">re</span>
 
<span class="n">emoticons_str</span> <span class="o">=</span> <span class="s2">r"""</span>
<span class="s2">    (?:</span>
<span class="s2">        [:=;] # Eyes</span>
<span class="s2">        [oO\-]? # Nose (optional)</span>
<span class="s2">        [D\)\]\(\]/\\OpP] # Mouth</span>
<span class="s2">    )"""</span>
 
<span class="n">regex_str</span> <span class="o">=</span> <span class="p">[</span>
    <span class="n">emoticons_str</span><span class="p">,</span>
    <span class="s1">r'&lt;[^&gt;]+&gt;'</span><span class="p">,</span> <span class="c1"># HTML tags</span>
    <span class="s1">r'(?:@[\w_]+)'</span><span class="p">,</span> <span class="c1"># @-mentions</span>
    <span class="s2">r"(?:\#+[\w_]+[\w\'_\-]*[\w_]+)"</span><span class="p">,</span> <span class="c1"># hash-tags</span>
    <span class="s1">r'http[s]?://(?:[a-z]|[0-9]|[$-_@.&amp;+]|[!*\(\),]|(?:%[0-9a-f][0-9a-f]))+'</span><span class="p">,</span> <span class="c1"># URLs</span>
 
    <span class="s1">r'(?:(?:\d+,?)+(?:\.?\d+)?)'</span><span class="p">,</span> <span class="c1"># numbers</span>
    <span class="s2">r"(?:[a-z][a-z'\-_]+[a-z])"</span><span class="p">,</span> <span class="c1"># words with - and '</span>
    <span class="s1">r'(?:[\w_]+)'</span><span class="p">,</span> <span class="c1"># other words</span>
    <span class="s1">r'(?:\S)'</span> <span class="c1"># anything else</span>
<span class="p">]</span>
    
<span class="n">tokens_re</span> <span class="o">=</span> <span class="n">re</span><span class="o">.</span><span class="n">compile</span><span class="p">(</span><span class="s1">r'('</span><span class="o">+</span><span class="s1">'|'</span><span class="o">.</span><span class="n">join</span><span class="p">(</span><span class="n">regex_str</span><span class="p">)</span><span class="o">+</span><span class="s1">')'</span><span class="p">,</span> <span class="n">re</span><span class="o">.</span><span class="n">VERBOSE</span> <span class="o">|</span> <span class="n">re</span><span class="o">.</span><span class="n">IGNORECASE</span><span class="p">)</span>
<span class="n">emoticon_re</span> <span class="o">=</span> <span class="n">re</span><span class="o">.</span><span class="n">compile</span><span class="p">(</span><span class="s1">r'^'</span><span class="o">+</span><span class="n">emoticons_str</span><span class="o">+</span><span class="s1">'$'</span><span class="p">,</span> <span class="n">re</span><span class="o">.</span><span class="n">VERBOSE</span> <span class="o">|</span> <span class="n">re</span><span class="o">.</span><span class="n">IGNORECASE</span><span class="p">)</span>
 
<span class="k">def</span> <span class="nf">tokenize</span><span class="p">(</span><span class="n">s</span><span class="p">):</span>
    <span class="k">return</span> <span class="n">tokens_re</span><span class="o">.</span><span class="n">findall</span><span class="p">(</span><span class="n">s</span><span class="p">)</span>
 
<span class="k">def</span> <span class="nf">preprocess</span><span class="p">(</span><span class="n">s</span><span class="p">,</span> <span class="n">lowercase</span><span class="o">=</span><span class="bp">False</span><span class="p">):</span>
    <span class="n">tokens</span> <span class="o">=</span> <span class="n">tokenize</span><span class="p">(</span><span class="n">s</span><span class="p">)</span>
    <span class="k">if</span> <span class="n">lowercase</span><span class="p">:</span>
        <span class="n">tokens</span> <span class="o">=</span> <span class="p">[</span><span class="n">token</span> <span class="k">if</span> <span class="n">emoticon_re</span><span class="o">.</span><span class="n">search</span><span class="p">(</span><span class="n">token</span><span class="p">)</span> <span class="k">else</span> <span class="n">token</span><span class="o">.</span><span class="n">lower</span><span class="p">()</span> <span class="k">for</span> <span class="n">token</span> <span class="ow">in</span> <span class="n">tokens</span><span class="p">]</span>
    <span class="k">return</span> <span class="n">tokens</span>
</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [ ]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython2">
              <pre><span class="n">wordlist</span><span class="o">=</span><span class="p">[]</span>
<span class="k">for</span> <span class="n">item</span> <span class="ow">in</span> <span class="n">df1</span><span class="p">[</span><span class="s1">'text'</span><span class="p">]:</span>
    <span class="k">if</span><span class="p">(</span><span class="nb">type</span><span class="p">(</span><span class="n">item</span><span class="p">)</span><span class="o">==</span><span class="nb">str</span><span class="p">):</span>
      <span class="n">wordlist</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">preprocess</span><span class="p">(</span><span class="n">item</span><span class="p">))</span>
    <span class="k">else</span><span class="p">:</span>
      <span class="k">continue</span>

<span class="n">wordlist</span> <span class="o">=</span> <span class="p">[</span><span class="n">item</span> <span class="k">for</span> <span class="n">sublist</span> <span class="ow">in</span> <span class="n">wordlist</span> <span class="k">for</span> <span class="n">item</span> <span class="ow">in</span> <span class="n">sublist</span><span class="p">]</span>
<span class="n">punctuation</span> <span class="o">=</span> <span class="nb">list</span><span class="p">(</span><span class="n">string</span><span class="o">.</span><span class="n">punctuation</span><span class="p">)</span>
<span class="n">stop</span> <span class="o">=</span> <span class="n">stopwords</span><span class="o">.</span><span class="n">words</span><span class="p">(</span><span class="s1">'english'</span><span class="p">)</span> <span class="o">+</span> <span class="n">punctuation</span> <span class="o">+</span> <span class="p">[</span><span class="s1">'rt'</span><span class="p">,</span> <span class="s1">'via'</span><span class="p">,</span><span class="s1">'com'</span><span class="p">,</span><span class="s1">'r'</span><span class="p">]</span>

<span class="n">wordlist</span> <span class="o">=</span> <span class="p">[</span><span class="n">item</span><span class="o">.</span><span class="n">lower</span><span class="p">()</span> <span class="k">for</span> <span class="n">item</span> <span class="ow">in</span> <span class="n">wordlist</span> <span class="k">if</span> <span class="n">item</span> <span class="ow">not</span> <span class="ow">in</span> <span class="n">stop</span><span class="p">]</span>
<span class="n">wordlist_nounicode</span> <span class="o">=</span><span class="p">[</span><span class="n">re</span><span class="o">.</span><span class="n">sub</span><span class="p">(</span><span class="s1">r'[^\x00-\x7F]+'</span><span class="p">,</span><span class="s1">''</span><span class="p">,</span> <span class="n">item</span><span class="p">)</span> <span class="k">for</span> <span class="n">item</span> <span class="ow">in</span> <span class="n">wordlist</span><span class="p">]</span>

<span class="c1"># Count hashtags only</span>
<span class="n">terms_hash</span> <span class="o">=</span> <span class="p">[</span><span class="n">term</span> <span class="k">for</span> <span class="n">term</span> <span class="ow">in</span> <span class="n">wordlist_nounicode</span> <span class="k">if</span> <span class="n">term</span><span class="o">.</span><span class="n">startswith</span><span class="p">(</span><span class="s1">'#'</span><span class="p">)]</span>
<span class="c1"># Count mention only</span>
<span class="n">terms_ment</span> <span class="o">=</span> <span class="p">[</span><span class="n">term</span> <span class="k">for</span> <span class="n">term</span> <span class="ow">in</span> <span class="n">wordlist_nounicode</span> <span class="k">if</span> <span class="n">term</span><span class="o">.</span><span class="n">startswith</span><span class="p">(</span><span class="s1">'@'</span><span class="p">)]</span>
<span class="c1"># Count terms only (no hashtags, no mentions)</span>
<span class="n">terms_only</span> <span class="o">=</span> <span class="p">[</span><span class="n">term</span> <span class="k">for</span> <span class="n">term</span> <span class="ow">in</span> <span class="n">wordlist_nounicode</span> <span class="k">if</span> <span class="n">term</span> <span class="ow">not</span> <span class="ow">in</span> <span class="n">stop</span> <span class="ow">and</span> <span class="ow">not</span> <span class="n">term</span><span class="o">.</span><span class="n">startswith</span><span class="p">((</span><span class="s1">'#'</span><span class="p">,</span> <span class="s1">'@'</span><span class="p">))]</span> 

<span class="n">count1</span> <span class="o">=</span> <span class="n">Counter</span><span class="p">()</span>
<span class="c1"># Update the counter</span>
<span class="n">count1</span><span class="o">.</span><span class="n">update</span><span class="p">(</span><span class="n">terms_hash</span><span class="p">)</span>

<span class="k">print</span> <span class="s2">"the first 40 most frequent hashtag:"</span>
<span class="k">print</span><span class="p">(</span><span class="n">count1</span><span class="o">.</span><span class="n">most_common</span><span class="p">(</span><span class="mi">40</span><span class="p">))</span>
<span class="k">print</span>
<span class="k">print</span>

<span class="n">count2</span> <span class="o">=</span> <span class="n">Counter</span><span class="p">()</span>
<span class="c1"># Update the counter</span>
<span class="n">count2</span><span class="o">.</span><span class="n">update</span><span class="p">(</span><span class="n">terms_ment</span><span class="p">)</span>

<span class="k">print</span> <span class="s2">"the first 10 most frequent mention:"</span>
<span class="k">print</span><span class="p">(</span><span class="n">count2</span><span class="o">.</span><span class="n">most_common</span><span class="p">(</span><span class="mi">40</span><span class="p">))</span>
<span class="k">print</span>
<span class="k">print</span>

<span class="n">count3</span> <span class="o">=</span> <span class="n">Counter</span><span class="p">()</span>
<span class="c1"># Update the counter</span>
<span class="n">count3</span><span class="o">.</span><span class="n">update</span><span class="p">(</span><span class="n">terms_only</span><span class="p">)</span>
<span class="k">print</span> <span class="s2">"the first 40 most frequent word:"</span>
<span class="k">print</span><span class="p">(</span><span class="n">count3</span><span class="o">.</span><span class="n">most_common</span><span class="p">(</span><span class="mi">41</span><span class="p">)[</span><span class="mi">1</span><span class="p">:])</span>
</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [21]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython2">
              <pre><span class="kn">import</span> <span class="nn">vincent</span> 
<span class="n">vincent</span><span class="o">.</span><span class="n">core</span><span class="o">.</span><span class="n">initialize_notebook</span><span class="p">()</span>

<span class="kn">from</span> <span class="nn">vincent</span> <span class="kn">import</span> <span class="n">AxisProperties</span><span class="p">,</span> <span class="n">PropertySet</span><span class="p">,</span> <span class="n">ValueRef</span>
<span class="n">word_freq</span> <span class="o">=</span> <span class="p">[(</span><span class="s1">'twitter'</span><span class="p">,</span> <span class="mi">38406</span><span class="p">),</span> <span class="p">(</span><span class="s1">'pic'</span><span class="p">,</span> <span class="mi">23536</span><span class="p">),</span> <span class="p">(</span><span class="s1">'halloween'</span><span class="p">,</span> <span class="mi">10795</span><span class="p">),</span> <span class="p">(</span><span class="s1">'video'</span><span class="p">,</span> <span class="mi">9545</span><span class="p">),</span> <span class="p">(</span><span class="s1">'new'</span><span class="p">,</span> <span class="mi">8537</span><span class="p">),</span> 
             <span class="p">(</span><span class="s1">'update'</span><span class="p">,</span> <span class="mi">7604</span><span class="p">),</span> <span class="p">(</span><span class="s1">'liked'</span><span class="p">,</span> <span class="mi">7068</span><span class="p">),</span> <span class="p">(</span><span class="s1">'event'</span><span class="p">,</span> <span class="mi">6850</span><span class="p">),</span> 
             <span class="p">(</span><span class="s1">'play'</span><span class="p">,</span> <span class="mi">5300</span><span class="p">),</span>  <span class="p">(</span><span class="s1">'get'</span><span class="p">,</span> <span class="mi">4227</span><span class="p">),</span> <span class="p">(</span><span class="s1">'like'</span><span class="p">,</span> <span class="mi">4135</span><span class="p">),</span> 
             <span class="p">(</span><span class="s1">'game'</span><span class="p">,</span> <span class="mi">4055</span><span class="p">),</span> <span class="p">(</span><span class="s1">'still'</span><span class="p">,</span> <span class="mi">3708</span><span class="p">),</span> 
             <span class="p">(</span><span class="s1">'candy'</span><span class="p">,</span> <span class="mi">3117</span><span class="p">),</span> <span class="p">(</span><span class="s2">"i'm"</span><span class="p">,</span> <span class="mi">3077</span><span class="p">),</span> <span class="p">(</span><span class="s1">'first'</span><span class="p">,</span> <span class="mi">2790</span><span class="p">),</span> 
             <span class="p">(</span><span class="s1">'catch'</span><span class="p">,</span> <span class="mi">2757</span><span class="p">),</span> <span class="p">(</span><span class="s1">'plus'</span><span class="p">,</span> <span class="mi">2705</span><span class="p">),</span> <span class="p">(</span><span class="s1">'hack'</span><span class="p">,</span> <span class="mi">2638</span><span class="p">),</span>  <span class="p">(</span><span class="s1">'niantic'</span><span class="p">,</span> <span class="mi">2587</span><span class="p">),</span> 
             <span class="p">(</span><span class="s1">'gym'</span><span class="p">,</span> <span class="mi">2378</span><span class="p">)]</span>

<span class="n">labels</span><span class="p">,</span> <span class="n">freq</span> <span class="o">=</span> <span class="nb">zip</span><span class="p">(</span><span class="o">*</span><span class="n">word_freq</span><span class="p">)</span>
<span class="n">data</span> <span class="o">=</span> <span class="p">{</span><span class="s1">'data'</span><span class="p">:</span> <span class="n">freq</span><span class="p">,</span> <span class="s1">'x'</span><span class="p">:</span> <span class="n">labels</span><span class="p">}</span>
<span class="n">bar</span> <span class="o">=</span> <span class="n">vincent</span><span class="o">.</span><span class="n">Bar</span><span class="p">(</span><span class="n">data</span><span class="p">,</span> <span class="n">iter_idx</span><span class="o">=</span><span class="s1">'x'</span><span class="p">)</span>
<span class="c1">#rotate x axis labels</span>
<span class="n">ax</span> <span class="o">=</span> <span class="n">AxisProperties</span><span class="p">(</span>
         <span class="n">labels</span> <span class="o">=</span> <span class="n">PropertySet</span><span class="p">(</span><span class="n">angle</span><span class="o">=</span><span class="n">ValueRef</span><span class="p">(</span><span class="n">value</span><span class="o">=-</span><span class="mi">30</span><span class="p">)))</span>
<span class="n">bar</span><span class="o">.</span><span class="n">axes</span><span class="p">[</span><span class="mi"></span><span class="p">]</span><span class="o">.</span><span class="n">properties</span> <span class="o">=</span> <span class="n">ax</span>
<span class="n">bar</span><span class="o">.</span><span class="n">display</span><span class="p">()</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt">
            </div>
            
            <div class="output_html rendered_html output_subarea ">
              <p>
              </p>
            </div>
          </div>
          
          <div class="output_area">
            <div class="prompt">
            </div>
            
            <div class="output_html rendered_html output_subarea ">
              <div id="visf17ea45185b14ccda60abdfec1fc07f5">
              </div>
              
              <p>
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [ ]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython2">
              <pre><span class="kn">from</span> <span class="nn">nltk</span> <span class="kn">import</span> <span class="n">bigrams</span> 

<span class="n">punctuation</span> <span class="o">=</span> <span class="nb">list</span><span class="p">(</span><span class="n">string</span><span class="o">.</span><span class="n">punctuation</span><span class="p">)</span>
<span class="n">stop</span> <span class="o">=</span> <span class="n">stopwords</span><span class="o">.</span><span class="n">words</span><span class="p">(</span><span class="s1">'english'</span><span class="p">)</span> <span class="o">+</span> <span class="n">punctuation</span> <span class="o">+</span> <span class="p">[</span><span class="s1">'rt'</span><span class="p">,</span> <span class="s1">'via'</span><span class="p">,</span><span class="s1">'com'</span><span class="p">,</span><span class="s1">'r'</span><span class="p">]</span>

<span class="n">wordlist_bigram</span><span class="o">=</span><span class="p">[]</span>
<span class="k">for</span> <span class="n">item</span> <span class="ow">in</span> <span class="n">df1</span><span class="p">[</span><span class="s1">'text'</span><span class="p">]:</span>
    <span class="k">if</span><span class="p">(</span><span class="nb">type</span><span class="p">(</span><span class="n">item</span><span class="p">)</span><span class="o">==</span><span class="nb">str</span><span class="p">):</span>
      <span class="n">tmplist</span> <span class="o">=</span> <span class="p">[</span><span class="n">term</span> <span class="k">for</span> <span class="n">term</span> <span class="ow">in</span> <span class="n">preprocess</span><span class="p">(</span><span class="n">item</span><span class="p">,</span><span class="n">lowercase</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span> <span class="k">if</span> <span class="n">term</span> <span class="ow">not</span> <span class="ow">in</span> <span class="n">stop</span><span class="p">]</span>
      <span class="c1">#tmplist = [re.sub(r'[^\x00-\x7F]+','', term) for term in item]        </span>
      <span class="k">for</span> <span class="n">term</span> <span class="ow">in</span> <span class="n">bigrams</span><span class="p">(</span><span class="n">tmplist</span><span class="p">):</span>
         <span class="n">wordlist_bigram</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="s1">' '</span><span class="o">.</span><span class="n">join</span><span class="p">(</span><span class="n">term</span><span class="p">))</span>
    <span class="k">else</span><span class="p">:</span>
      <span class="k">continue</span>
</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [ ]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython2">
              <pre><span class="n">count</span> <span class="o">=</span> <span class="n">Counter</span><span class="p">()</span>
<span class="c1"># Update the counter</span>
<span class="n">count</span><span class="o">.</span><span class="n">update</span><span class="p">(</span><span class="n">wordlist_bigram</span><span class="p">)</span>
<span class="k">print</span> <span class="s2">"the first 40 most frequent word:"</span>
<span class="k">print</span><span class="p">(</span><span class="n">count</span><span class="o">.</span><span class="n">most_common</span><span class="p">(</span><span class="mi">1000</span><span class="p">))</span>
</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [ ]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython2">
              <pre><span class="kn">import</span> <span class="nn">cPickle</span> <span class="kn">as</span> <span class="nn">pickle</span>
<span class="c1">#pickle.dump(wordlist_nounicode, open( "word_onegram.p", "wb" ) )</span>
<span class="c1">#pickle.dump(terms_only, open( "terms_only.p", "wb" ) )</span>
<span class="c1">#pickle.dump( wordlist_bigram, open( "word_bigram.p", "wb" ) )</span>

<span class="n">terms_only</span> <span class="o">=</span> <span class="n">pickle</span><span class="o">.</span><span class="n">load</span><span class="p">(</span> <span class="nb">open</span><span class="p">(</span> <span class="s2">"terms_only.p"</span><span class="p">,</span> <span class="s2">"rb"</span> <span class="p">)</span> <span class="p">)</span>
<span class="c1">#wordlist_nounicode = pickle.load( open( "word_onegram.p", "rb" ) )</span>
<span class="c1">#wordlist_bigram = pickle.load( open( "word_bigram.p", "rb" ) )</span>
</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <p>
            Other rankings as follows:
          </p>
          
          <p>
            the first 20 most frequent hashtag
          </p>
          
          <p>
            *(&#8216;#pokemongo&#8217;, 45988), (&#8216;#pokemon&#8217;, 6280), (&#8216;#funny&#8217;, 3757), (&#8216;#minecraft&#8217;, 3723), (&#8216;#agario&#8217;, 3703), (&#8216;#amazing&#8217;, 3695), (&#8216;#game&#8217;, 3501), (&#8216;#new&#8217;, 3342), (&#8216;#europe&#8217;, 3319), (&#8216;#turkey&#8217;, 3319), (&#8216;#trolling&#8217;, 3318), (&#8216;#love&#8217;, 2584), (&#8216;#pok&#8217;, 2055), (&#8216;#gaming&#8217;, 1163), (&#8216;#pokeballs&#8217;, 1053), (&#8216;#pokemongocoinspic&#8217;, 1015), (&#8216;#teamvalor&#8217;, 779), (&#8216;#pokecoins&#8217;, 605), (&#8216;#tech&#8217;, 601), (&#8216;#halloween&#8217;, 555)
          </p>
          
          <p>
            the first 10 most frequent mention
          </p>
          
          <p>
            *(&#8216;@youtube&#8217;, 9318), (&#8216;@leafyishere&#8217;, 1304), (&#8216;@omgitsalia&#8217;, 1239), (&#8216;@pokemongoapp&#8217;, 1210), (&#8216;@trnrtips&#8217;, 1029), (&#8216;@nianticlabs&#8217;, 907), (&#8216;@fsu_atl&#8217;, 522), (&#8216;@lachlanyt&#8217;, 301), (&#8216;@suknives&#8217;, 286), (&#8216;@witelightinghwd&#8217;, 222)
          </p>
          
          <p>
            A search based on bi-gram gives the first 20 most frequent two adjacent words:
          </p>
          
          <p>
            *(&#8216;pic twitter&#8217;, 23446), (&#8216;@youtube video&#8217;, 7179), (&#8216;#pokemongo pic&#8217;, 4509), (&#8216;halloween event&#8217;, 3673), (&#8216;#game #trolling&#8217;, 3318), (&#8216;play pokemon&#8217;, 2750), (&#8216;go update&#8217;, 2228), (&#8216;#love #amazing&#8217;, 2199), (&#8216;new pokemon&#8217;, 1497), (&#8216;halloween update&#8217;, 1182), (&#8216;celebrates halloween&#8217;, 968), (&#8216;need pokecoins&#8217;, 911), (&#8216;rare pokemon&#8217;, 814), (&#8216;apple pen&#8217;, 768), (&#8216;pine apple&#8217;, 764), (&#8216;ppap pine&#8217;, 764), (&#8216;still play&#8217;, 747), (&#8216;still playing&#8217;, 744), (&#8216;candy count&#8217;, 695), (&#8216;go cheats&#8217;, 685)
          </p>
          
          <p>
            which indicates that
          </p>
          
          <ul>
            <li>
              Pokemon Go players and sellers use twitter and youtube frequently;
            </li>
            <li>
              recent update and event also show up timely in tweets;
            </li>
            <li>
              tweets show great need of pokecoins, candy and rare species etc. which might poses difficulties for current and potential users;
            </li>
            <li>
              Pokemon Go game is very addictive as people like to use phrases such as &#8216;still play/playing&#8217;.
            </li>
            <li>
              Pokemon Go&#8217;s influence even reaches popular songs (e.g., Pen Pineapple Apple Pen).
            </li>
          </ul>
          
          <p>
            To sum up the finding, Pokemon Go clearly has very good and successful marketing strategies to stimulate their players such as holding events, and sharing pic/movies with/among the users. It is also integrated in the pop culture very well in which the game can benefit from. Certain needs such as pokecoins and rare species might pose difficulties for current and potential players, and the effects of that should be further investigated.
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [15]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython2">
              <pre><span class="c1"># save to json file and then host the plot with webserver; abandoned</span>

<span class="kn">import</span> <span class="nn">vincent</span> 
<span class="kn">from</span> <span class="nn">vincent</span> <span class="kn">import</span> <span class="n">AxisProperties</span><span class="p">,</span> <span class="n">PropertySet</span><span class="p">,</span> <span class="n">ValueRef</span>
<span class="n">word_freq</span> <span class="o">=</span> <span class="p">[(</span><span class="s1">'twitter'</span><span class="p">,</span> <span class="mi">38406</span><span class="p">),</span> <span class="p">(</span><span class="s1">'pic'</span><span class="p">,</span> <span class="mi">23536</span><span class="p">),</span> <span class="p">(</span><span class="s1">'halloween'</span><span class="p">,</span> <span class="mi">10795</span><span class="p">),</span> <span class="p">(</span><span class="s1">'video'</span><span class="p">,</span> <span class="mi">9545</span><span class="p">),</span> <span class="p">(</span><span class="s1">'new'</span><span class="p">,</span> <span class="mi">8537</span><span class="p">),</span> 
             <span class="p">(</span><span class="s1">'update'</span><span class="p">,</span> <span class="mi">7604</span><span class="p">),</span> <span class="p">(</span><span class="s1">'liked'</span><span class="p">,</span> <span class="mi">7068</span><span class="p">),</span> <span class="p">(</span><span class="s1">'event'</span><span class="p">,</span> <span class="mi">6850</span><span class="p">),</span> 
             <span class="p">(</span><span class="s1">'play'</span><span class="p">,</span> <span class="mi">5300</span><span class="p">),</span>  <span class="p">(</span><span class="s1">'get'</span><span class="p">,</span> <span class="mi">4227</span><span class="p">),</span> <span class="p">(</span><span class="s1">'like'</span><span class="p">,</span> <span class="mi">4135</span><span class="p">),</span> 
             <span class="p">(</span><span class="s1">'game'</span><span class="p">,</span> <span class="mi">4055</span><span class="p">),</span> <span class="p">(</span><span class="s1">'still'</span><span class="p">,</span> <span class="mi">3708</span><span class="p">),</span> 
             <span class="p">(</span><span class="s1">'candy'</span><span class="p">,</span> <span class="mi">3117</span><span class="p">),</span> <span class="p">(</span><span class="s2">"i'm"</span><span class="p">,</span> <span class="mi">3077</span><span class="p">),</span> <span class="p">(</span><span class="s1">'first'</span><span class="p">,</span> <span class="mi">2790</span><span class="p">),</span> 
             <span class="p">(</span><span class="s1">'catch'</span><span class="p">,</span> <span class="mi">2757</span><span class="p">),</span> <span class="p">(</span><span class="s1">'plus'</span><span class="p">,</span> <span class="mi">2705</span><span class="p">),</span> <span class="p">(</span><span class="s1">'hack'</span><span class="p">,</span> <span class="mi">2638</span><span class="p">),</span>  <span class="p">(</span><span class="s1">'niantic'</span><span class="p">,</span> <span class="mi">2587</span><span class="p">),</span> 
             <span class="p">(</span><span class="s1">'gym'</span><span class="p">,</span> <span class="mi">2378</span><span class="p">)]</span>

<span class="n">labels</span><span class="p">,</span> <span class="n">freq</span> <span class="o">=</span> <span class="nb">zip</span><span class="p">(</span><span class="o">*</span><span class="n">word_freq</span><span class="p">)</span>
<span class="n">data</span> <span class="o">=</span> <span class="p">{</span><span class="s1">'data'</span><span class="p">:</span> <span class="n">freq</span><span class="p">,</span> <span class="s1">'x'</span><span class="p">:</span> <span class="n">labels</span><span class="p">}</span>
<span class="n">bar</span> <span class="o">=</span> <span class="n">vincent</span><span class="o">.</span><span class="n">Bar</span><span class="p">(</span><span class="n">data</span><span class="p">,</span> <span class="n">iter_idx</span><span class="o">=</span><span class="s1">'x'</span><span class="p">)</span>
<span class="c1">#rotate x axis labels</span>
<span class="n">ax</span> <span class="o">=</span> <span class="n">AxisProperties</span><span class="p">(</span>
         <span class="n">labels</span> <span class="o">=</span> <span class="n">PropertySet</span><span class="p">(</span><span class="n">angle</span><span class="o">=</span><span class="n">ValueRef</span><span class="p">(</span><span class="n">value</span><span class="o">=-</span><span class="mi">30</span><span class="p">)))</span>
<span class="n">bar</span><span class="o">.</span><span class="n">axes</span><span class="p">[</span><span class="mi"></span><span class="p">]</span><span class="o">.</span><span class="n">properties</span> <span class="o">=</span> <span class="n">ax</span>

<span class="n">bar</span><span class="o">.</span><span class="n">to_json</span><span class="p">(</span><span class="s1">'term_freq.json'</span><span class="p">)</span>
</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <h2 id="3-2.-daily-pattern">
            4-2. sentiment analysis<a class="anchor-link" href="#4.-Sentiment-analysis">¶</a>
          </h2>
          
          <p>
            We can try to measure the sentiment scores of the tweets about Pokemon Go, which provides a way to tell game players&#8217; opinion about the game. We use the same data sample as above, but only use the most recent 4000 tweets as a test and run those tweets through a <a href="http://pythonhosted.org/sentiment_classifier/">sentiment classifier</a> built base on Word Sense Disambiguation using wordnet and word occurance statistics from nltk.
          </p>
          
          <ul>
            <li>
              Based on the 4000 tweets, we find a much greater positive score ($85.6$) than the total negative score ($33.9$), indicates Pokemon Go is overall receiving a very positive feedback.
            </li>
          </ul>
          
          <p>
            Similar analysis can be applied to other games too, and a comparison among a pool of mobile games would also show how much people like the games.
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [22]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython2">
              <pre><span class="kn">import</span> <span class="nn">cPickle</span> <span class="kn">as</span> <span class="nn">pickle</span>

<span class="n">terms_only</span> <span class="o">=</span> <span class="n">pickle</span><span class="o">.</span><span class="n">load</span><span class="p">(</span> <span class="nb">open</span><span class="p">(</span> <span class="s2">"terms_only.p"</span><span class="p">,</span> <span class="s2">"rb"</span> <span class="p">)</span> <span class="p">)</span>
</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [35]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython2">
              <pre><span class="kn">from</span> <span class="nn">senti_classifier</span> <span class="kn">import</span> <span class="n">senti_classifier</span>


<span class="n">pos_score</span><span class="p">,</span> <span class="n">neg_score</span> <span class="o">=</span> <span class="n">senti_classifier</span><span class="o">.</span><span class="n">polarity_scores</span><span class="p">(</span><span class="n">terms_only</span><span class="p">[</span><span class="o">-</span><span class="mi">4000</span><span class="p">:])</span>
<span class="k">print</span> <span class="n">pos_score</span><span class="p">,</span> <span class="n">neg_score</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt">
            </div>
            
            <div class="output_subarea output_stream output_stdout output_text">
              <pre>85.625 33.931
</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <h1 id="5.-Summary">
            5. Summary<a class="anchor-link" href="#5.-Summary">¶</a>
          </h1>
          
          <p>
            In this proposal, I have demonstrated that we could make use of the data from Twitter to gain insight in the mobile game industry.
          </p>
          
          <ul>
            <li>
              We can perform very efficient and productive survey, which benifits both the game development and marketing
            </li>
            <li>
              We can also perform detailed analysis on given product (here use Pokemon Go as an example) to find out important information such as hot terms/topic, product usage patterns, and the customer&#8217;s opinion of the product.
            </li>
          </ul>
          
          <p>
            Further improvement:
          </p>
          
          <ul>
            <li>
              bigger data set and larger sample of mobile games
            </li>
            <li>
              distinguish tweets from different categories, such as original post or retweet, ads or sale, etc.
            </li>
            <li>
              quantitative measure of the relationship between the twitter users and the real game players
            </li>
          </ul>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In [ ]:
        </div>
        
        <div class="inner_cell">
        </div>
      </div>
    </div>
  </div>
</div>

&nbsp;
