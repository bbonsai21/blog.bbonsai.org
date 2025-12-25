# Why is this the first blog post?

I wanted to share with the World Wide Web how I managed to put up something of mine, and explain how easily it can be replicated.
<br>
I have no experience in web development and I have no intentions whatsoever of becoming a web developer. This is the ultimate proof one
doesn't need to be skilled to put up something of his own.

# Who is BlueBonsai?

Check [me](https://bbonsai.org) out.

# How does my website function?

Simplicity was what I wanted the moment I put my hands my domain.<br>
Here you find no weird web frameworks that hide 300 operations under the hood:
the weirdest thing you might come across is a .js fetch script that loads .md files so that they're displayed to the user,
and I don't think that's fancy.<br>
I am not a web developer, nor I have any desire for better styling: the 'retro' style (particularly, [this](https://cv.bbonsai.org)) is very
nice on its own, and it doesn't require anything else to look great.
<br>

# Where do I host my pages?

Everything is being hosted on my [Github](https://github.com/bbonsai21), via [Github pages](https://docs.github.com/en/pages).
Only real cost is the domain: we're talking about 1 euro a month for the next 10 years - a risible sum.
I bought it on [Porkbun](https://porkbun.com). Check it out!

# How does Porkbun function?

To get yourself a domain you'll need a domain seller. Porkbun does this, for decent prices. Other famous domain sellers are:<br>
- [GoDaddy](https://godaddy.com) (yeah, I know...)
- [Namecheap](https://namecheap.com)

I used porkbun because I received good reviews from other users and their maintaining team is pretty friendly (they are pretty hilarious).
<br>
But how does it work? First off, go to their website. Check if the domain you want is present there. If not, you'll better use the original
domain seller. If it's present, check the price. Usually prices are reported on a yearly basis. You can put the domain in your cart and checkout.
<br>
To manage a domain you will NEED an account: it's where your settings will live and will be manageable. Better not lose it.
<br>
After having bought the domain (typical payment media are credit and debit cards, pre-paid cards and even crypto-currencies) you'll have to set it
up by clicking the `DNS` option in the domain manager menu, right below your domain name. This will open up another menu where you'll be abe to
select a few settings. Typically, you can pull it off with simply clicking the pre-made "Github" DNS option, that will pop-up an input box
where you can insert the name of your repo, and that's about it. Better watch a video on this topic, that'll cover it better than what text can do.
<br>
Very important is, then, allowing Github display your domain upon connection to your website. How does it work?
I recommend you FIRST OF ALL verify the ownership of the domain in your account settings, so that you'll prevent other attaching to your own domain.
You do that by going to your Github Settings > Pages (on the left menu, after having scrolled down a bit) > Add a domain. From here follow
the steps presented to you by the Github page.
<br>
After this you're ready to connect your webpage repo to your domain:<br>
1. go to your repo<br>
2. open repo Settings<br>
3. Pages<br>
4. set the branch to master<br>
5. add your custom domain as `https://your-domain.postfix` (e.g. `https://bbonsai.org` - no need of the `www.` subdomain prefix)<br>
6. wait for it to complete the verification<br>
7. tick `Enforce HTTPS`.<br>
<br>
Please, notice that options 5-7 could take some minutes for them to complete. Don't panic if it's not instantaneous. Wait until Github gives 
you the OK to proceed.<br>
If you encounter a problem during any of these steps, best thing is to either browse it or ask an LLM model. I have played with both until
I managed to do everything right.<br>
Notice, again, that this process works for setting up domains and sub-domains, but for for sub-domains you'll need to add a slightly different
DNS configuration: you'll have to set the ALIAS to have the subdomain you wish to utilise (e.g. you're reading this post on
**blog**.bbonsai.org - my main domain is bbonsai; another sub-domain I have is **cv**).
<br>
In any case - if you are stuck and an LLM doesn't help, please feel free to [contact me](https://cv.bbonsai.org) anytime!

<br>
<br>

# How do I manage the website?

I don't have much of a burden on my shoulders. I simply have to do the following:<br>
1. Open desktop terminal
2. `archive` to update the archive, `archive-save` to push it to Github. `blog [post_name]` to write a new blog post (or modify an existing one)
and `blog-save` to push it to Github.
<br>
Clearly, this works very well if you've set up the right commands. Here's how to do it on Linux (to do it on Windows or other systems, it's up to
you translating the following to your OS-specific bash-like language [^1]):<br>

Here we presume you already have a Github page; then, create a folder anywhere you wish to keep your website locally, and type:

```bash
cd [your-local-folder-path]
git pull [link-to-your-github-repo]
```

Now comes the fun:

```bash
cd [your-repo]
nano ~/.bashrc
```

And add the following to the end of the bash file:

```bash
# Create or modify blog post
blog() {
    cd "absolute/path/to/your/repo" || return
    local FILE=$1
    if [ -z "$FILE" ]; then 
        echo "Please specify a filename (e.g., blog post1.md)"
    else
        nano "$FILE"
    fi
    cd - > /dev/null
}

# Save and push blog
blog-save() {
    local MSG=$1
    if [ -z "$MSG" ]; then MSG="New blog post update"; fi

    cd "absolute/path/to/your/repo" || return
    git add .
    git commit -m "$MSG"
    git push
    echo "Blog synchronised."
    cd - > /dev/null
}
```

And that's about it. This clearly implies you understand a bit of `bash` and `git`, besides some `Github`.
If you do not, please consider learning more about them (either browser the Internet or ask an AI to explain in great detail - they'll both
do better explaining than whatever I could ever do myself).
<br>
<br>

# Final notes

As previously states, some operations might require time to complete. Others, instead, can have infinite time and never complete.<br>
Here we have 2 possibilities: you have done something wrong or the tool you're using may be damned. I've had experience with both, so let's try
to uncover some possible mistakes you might happen to do during the setup process:<br>
1. incorrect DNS configuration - there is nothing much that can be done here. The process has to be done cautiously, but domain sellers offer
the tools for a faster setup so that you minimise errors. Use them, if you are uncertain. If even after using them you get errors, don't
be afraid of *nuking* the DNS settings: they can be set back anytime without any issue. Follow carefully the steps on this page and on other
more detailed pages for the right results.<br>
2. apparently correct DNS setup but website doesn't point where it should: well, this is entirely up to you to verify. You must be certain
your page is pointing to the Github repo. Remember the Github repo must have a website setup (an index.html and, ideally, a CNAME - this one
is set up by Github upon domain configuration in the Pages window, so no worries).
3. certainly correct DNS setup but website doesn't point where it should: gulp! THis is annoying. How about you try opening up your link in an
private window of your browser? If it doesn't work, try also re-opening the browser itself or adding something like `/?v=n`, where n
is any number youy can think of, at the end of your link. Why this? Well, the answer is ... browser website caching! Yup, I said it. Something that's
as useful as scary; your browser is kind of lazy, so not to send requests all the time it likes to cache up certain pages and to retrieve those
upon request. What's the matter, you ask? Well, good luck seeing your changes if your browser keeps thinking the website is the same and gives you
the old page. Until the cache is present, the old website remains there, and you won't see changes. When this happens I either use the link trick
(that forces the browser to send a new request, since the link is "new") or I open up the webpage from my phone
(that I hopefully haven't used before on the same webpage, else also that there is probably cached - lmao) or, in alternative, the private window.
Notice this isn't jsut a problem with website's content, but also with its security certificates: your website will fully cache also the
HTTPS certificate, so if your website was unsecure it may appear unsafe also now that you have set up a certificate correctly.

<br>
<br>

# Projects for the blog

I don't have many interesting things to say, but sometimes I feel the urge to talk to someone, and the blog is all about that: me talking to my
virtual friends. And, altough I don't know who (if someone!) reads me, but I'm glad I can share a bit of myself with whoever dedicates me a bit
of their time. That's the greatest of all honours: being part of someone else's thoughts.
<br>
Have a prosperous life, Internet.

[1]: [Here](https://learn.microsoft.com/en-us/windows/wsl/install) is a possible solution!
