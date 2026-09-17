FROM texlive/texlive:latest

# The `ctan` alias resolves through mirror.ctan.org's round-robin, which regularly
# hands back a mirror that cannot serve texlive.tlpdb -- the build then either fails
# outright or hangs for minutes before failing. Walk specific mirrors instead.
RUN for repo in \
      https://mirror.clarkson.edu/ctan/systems/texlive/tlnet \
      https://mirrors.rit.edu/CTAN/systems/texlive/tlnet \
      https://ctan.math.illinois.edu/systems/texlive/tlnet ; \
    do \
      tlmgr option repository "$repo" && \
      tlmgr update --self && \
      tlmgr install \
        enumitem \
        titlesec \
        xcharter \
        xcharter-math \
        fontaxes \
        etoolbox \
        xstring \
        geometry \
        fancyhdr \
        xkeyval \
        microtype \
        hyperxmp \
        datetime2 \
        datetime2-english \
        embedfile && \
      exit 0 ; \
    done ; \
    echo "no CTAN mirror served the package database" >&2 ; \
    exit 1

WORKDIR /data
ENTRYPOINT ["pdflatex"]
