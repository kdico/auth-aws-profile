FROM public.ecr.aws/sam/build-python3.12:1

RUN set -eux; \
    dnf -y update; \ 
    dnf clean all; \
    python3 -m pip install --user pipx; \
    python3 -m pipx ensurepath; \
    source ~/.bashrc; \
    pipx install poetry==1.2.0; \
    poetry config virtualenvs.in-project true;
