This article is intended to introduce Tennessee Tech's HPC users to
common Spack usage. If the materials covered here do not answer your
questions or you need additional assistance, please complete the [HPC
Issues
Ticket](https://services.tntech.edu/TDClient/1878/Portal/Requests/TicketRequests/NewForm?ID=s2jbAC%7eEZU8_&RequestorType=Service).

If you have not yet requested access to the HPC and you would like to do
so, please complete the [HPC Access Request
Form](https://services.tntech.edu/TDClient/1878/Portal/Requests/TicketRequests/NewForm?ID=EwwIhDonRRw_&RequestorType=Service). 

## Suggested Reading Order

-   [Introduction to Tennessee Tech University's High Performance
    Computer](https://services.tntech.edu/TDClient/1878/Portal/KB/ArticleDet?ID=134358) 
-   [HPC Interactive ](https://services.tntech.edu/TDClient/1878/Portal/KB/ArticleDet?ID=134361)
-   [HPC: Batch
    Jobs](https://services.tntech.edu/TDClient/1878/Portal/KB/ArticleDet?ID=134374)
-   [Spack Quick
    Reference](https://services.tntech.edu/TDClient/1878/Portal/KB/ArticleDet?ID=134376)
-   [SLURM and HPCShell Quick
    Reference](https://services.tntech.edu/TDClient/1878/Portal/KB/ArticleDet?ID=134379)
-   [Using
    Containers](https://services.tntech.edu/TDClient/1878/Portal/KB/ArticleDet?ID=112569)

## Other Suggested Reading and Helpful Resources

-   [Open OnDemand for
    HPC](https://services.tntech.edu/TDClient/1878/Portal/KB/ArticleDet?ID=134382)
-   [HPC - Open OnDemand Application -
    Jupyter Notebooks](https://services.tntech.edu/TDClient/1878/Portal/KB/ArticleDet?ID=134542)
-   [Science
    DMZ](https://services.tntech.edu/TDClient/1878/Portal/KB/ArticleDet?ID=134444)
-   [HPC Job
    Scheduling](https://services.tntech.edu/TDClient/1878/Portal/KB/ArticleDet?ID=112543)
-   [Submitting Groups of HPC Jobs with Job
    Arrays](https://services.tntech.edu/TDClient/1878/Portal/KB/ArticleDet?ID=112568)
-   [HPC Spack Package
    Request](https://services.tntech.edu/TDClient/1878/Portal/Requests/ServiceDet?ID=50539)

## Overview

-   [What is Spack?](#WhatIsSpack)
-   [Common Spack Commands and Arguments](#SpackCommands)
-   [Changing Your Spack Version](#Changing%20Spack%20Version)
    -   [Changing Spack Version On An As-Needed
        Basis](#Subheader:%20Changing%20Spack%20Version%20on%20an%20As-needed%20Basis)
    -   [Changing Your Personal Default
        Spack Version](#Subheader:%20Changing%20Your%20Personal%20Default%20Version%20of%20Spack)
-   [Spack List vs Spack Find](#Spack%C2%A0List%20vs%20Spack%C2%A0Find)
    -   [Spack Info](#Subheader:%20Spack%20Find)
    -   [Spack Load](#Spack%20Load)
-   [Specifying Versions and Dependencies](#VersionsAndDependencies)
-   [Chaining From Centrally-Managed to User-Managed
    Installations](#Chaining)

## <span id="WhatIsSpack">What is Spack?</span>

Spack is a flexible package management tool designed to support multiple
versions and configurations of software on a wide variety of platforms
and environments. It was designed for large supercomputing centers.  You
may search for available packages at <https://packages.spack.io/>.  

For additional understanding, we recommend the following
Spack documentation:

-   <a
    href="https://spack.readthedocs.io/en/latest/basic_usage.html#listing-available-packages"
    aria-label="Link https://spack.readthedocs.io/en/latest/basic_usage.html#listing-available-packages"
    rel="noreferrer noopener" target="_blank"
    title="https://spack.readthedocs.io/en/latest/basic_usage.html#listing-available-packages">https://spack.readthedocs.io/en/latest/basic_usage.html#listing-available-packages</a>
-   <a
    href="https://spack.readthedocs.io/en/latest/basic_usage.html#spack-find"
    aria-label="Link https://spack.readthedocs.io/en/latest/basic_usage.html#spack-find"
    rel="noreferrer noopener" target="_blank"
    title="https://spack.readthedocs.io/en/latest/basic_usage.html#spack-find">https://spack.readthedocs.io/en/latest/basic_usage.html#spack-find</a>
-   <a
    href="https://spack.readthedocs.io/en/latest/basic_usage.html#using-installed-packages"
    aria-label="Link https://spack.readthedocs.io/en/latest/basic_usage.html#using-installed-packages"
    rel="noreferrer noopener" target="_blank"
    title="https://spack.readthedocs.io/en/latest/basic_usage.html#using-installed-packages">https://spack.readthedocs.io/en/latest/basic_usage.html#using-installed-packages</a>

## <span id="SpackCommands">Spack Commands and Arguments</span>

<table class="table table-striped table-hover table-bordered"
style="width: 100%;">
<thead>
<tr class="header">
<th scope="col" style="width: 200px"><p>Command/Argument</p></th>
<th scope="col">Description</th>
<th scope="col" style="width: 250px">Example</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>spack --help</td>
<td>Provides the manual page for the specified command. </td>
<td>spack --help, spack spec --help</td>
</tr>
<tr class="even">
<td>spack list &lt;package_name&gt;</td>
<td>List and search available packages. The package name is optional.
For a complete list of all available packages 'spack list'. *</td>
<td>spack list tensorflow</td>
</tr>
<tr class="odd">
<td>spack info &lt;package_name&gt;</td>
<td>Get detailed information on a particular package.</td>
<td>spack info --all mpich</td>
</tr>
<tr class="even">
<td>spack find &lt;package_name&gt;</td>
<td>List and search packages that are currently installed in the HPC.
The package name is optional, leaving it off will produce a complete
list of all packages currently installed in the HPC.**</td>
<td>spack find gatk, spack find --loaded</td>
</tr>
<tr class="odd">
<td>spack spec &lt;package_name&gt;</td>
<td>Provides information on the specific dependencies. </td>
<td>spack spec py-keras</td>
</tr>
<tr class="even">
<td>spack install &lt;package_name&gt;</td>
<td>Locally install a Spack package. If this is a package that multiple
user will need, please reach out to the HPC Administrator to have it
installed globally. </td>
<td>spack install circos</td>
</tr>
<tr class="odd">
<td>spack load &lt;package_name&gt;</td>
<td>Add package to the user environment. </td>
<td>spack load picard</td>
</tr>
</tbody>
</table>

\*Note: You may also search for packages
at <https://packages.spack.io/>. 

\*\*Note: If you do not find the package that you need using 'spack
find' but it is available using 'spack list' we are able to install the
package for your use. Please contact the HPC Administrator. 

## <span id="Changing Spack Version">Changing Your Spack Version</span>

We have been using Spack for package management on the HPC for a while
now and, as a result, there are different versions available to be used.
The default version of Spack is USUALLY the most recent version that we
have available that is also completely set up with all of the necessary
packages, however you may find it necessary to change the version that
you are working in. Here, I will show two ways to do this. 

### <span id="Subheader: Changing Spack Version on an As-needed Basis">Changing Spack Version On An As-Needed Basis</span>

Perhaps you only want to change your version occasionally and mostly
work in the default version. This change must be made every time you
open a new terminal and it applies only to the terminal you are working
in at the moment.

To begin, I want to check the Spack version that I am currently in. I
will do this by using the command <span
style="background-color:#fff0f5;">`` `which  ``</span><span
style="background-color:#fff0f5;">`spack`</span><span
style="background-color:#fff0f5;">`` ` ``</span>. Here is the result
that I see but yours may be slightly different:


    [sw-slcolson@gpunode003 hpcadmins]$ which spack

    spack ()

    {

        : this is a shell function from: /opt/ohpc/pub/spack/v0.20.1/share/spack/setup-env.sh;

        : the real spack script is here: /opt/ohpc/pub/spack/v0.20.1/bin/spack;

        _spack_shell_wrapper "$@";

        return $?

    }

    [sw-slcolson@gpunode003 hpcadmins]$

Currently, I am in Spack version V0.20.1 but I would really like to work
in Spack version V0.21.1 today. To change this I am going to run the
following command:


    . /opt/ohpc/pub/spack/v0.21.1/share/spack/setup-env.sh

Now that I have done this, I check that the change was successful by
running the <span
style="background-color:#fff0f5;">`` `which  ``</span><span
style="background-color:#fff0f5;">`spack`</span><span
style="background-color:#fff0f5;">`` ` ``</span> command again. Here is
the new result:


    [sw-slcolson@gpunode003 hpcadmins]$ which spack

    spack ()

    { 

        : this is a shell function from: /opt/ohpc/pub/spack/v0.21.1/share/spack/setup-env.sh;

        : the real spack script is here: /opt/ohpc/pub/spack/v0.21.1/bin/spack;

        _spack_shell_wrapper "$@";

        return $?

    }

This looks good and I am now ready to proceed with my project!

### <span id="Subheader: Changing Your Personal Default Version of Spack">Changing Your Personal Default Spack Version</span>

You may decide to change your personal default Spack version if you find
that you are exclusively working in another version of Spack that is not
the system default. If this case, you may do so by making a change to a
file in your home directory named <span
style="background-color:#fff0f5;">`` `. ``</span><span
style="background-color:#fff0f5;">`spack`</span><span
style="background-color:#fff0f5;">`` _setup` ``</span>. (Note: The
period before the name makes it invisible to you most of the time.) The
way that we are going to change this file is by using a text editor
called Nano, which is installed by default on the HPC. 


    [sw-slcolson@gpunode003 hpcadmins]$ nano ~/.spack_setup

Note that when you do this, a new screen is going to open. Don't panic,
that is normal. 

I want to set my default Spack version to V0.21.1. To do this, I need to
add one line to this file:


    SPACK_VER=v0.21.1

Here is what that should look like:

<img
src="https://services.tntech.edu/TDPortal/Images/Viewer?fileName=19be5906-6050-480a-87d1-1c224c2adb17.png&amp;beidInt=386"
class="img-responsive" style="width: 600px; height: 581px;"
alt="Reference Image of Text Editor Screen " />

Notice, that there are instructions at the bottom of the screen that
will help you if you need them. For now, I only want to save and exit
the text editor and go back to my terminal session. To do so I will hit
my control button (for Windows) or command button (for Mac) and my <span
style="background-color:#fff0f5;">`` `x` ``</span> key <span
style="background-color:#ffff00;">at the same time</span>. When I do
this, the bottom of the screen will change to look like this:

<img
src="https://services.tntech.edu/TDPortal/Images/Viewer?fileName=768ace80-9cbe-4ac0-a517-6008bb60b648.png&amp;beidInt=386"
class="img-responsive" style="width: 600px; height: 43px;"
alt="Reference Image Showing the Save Prompt in Nano Text Editor" />

I will press <span style="background-color:#fff0f5;">`` `y` ``</span> to
save and the file will save and exit. 

Now I will need to restart my terminal for the change to be effective,
but I will only have to change my Spack version when I don't want to be
working in Spack V0.21.1 any longer. 

## <span id="Spack List vs Spack Find">Spack List vs Spack Find</span>

For this section, I will use a python library known to most people as
Tensorflow. 

To check if a specific Spack package is installed in the Tennessee Tech
HPC the \`spack find\` command is necessary. Let's check it out:


    [sw-slcolson@gpunode003 hpcadmins]$ spack find tensorflow

    ==> No package matches the query: tensorflow

Hmmm... that doesn't seem right. 

The command <span style="background-color:#fff0f5;">`` ` ``</span><span
style="background-color:#fff0f5;">`spack`</span><span
style="background-color:#fff0f5;">``  find` ``</span> has a drawback. It
can only tell you if that package (exactly as it is spelled) is
available on the TN Tech HPC. It cannot tell you if the name is
incorrect and it cannot tell you if the package is available as a
Spack package in general and just not installed on OUR system. 

Let's try it with \`spack list\` instead:


    [sw-slcolson@gpunode003 hpcadmins]$ spack list tensorflow

    py-tensorflow py-tensorflow-estimator py-tensorflow-metadata tensorflow-serving-client

    py-tensorflow-datasets py-tensorflow-hub py-tensorflow-probability

Ahhh... there it is! You can also try truncating the name ( <span
style="background-color:#fff0f5;">`` ` ``</span><span
style="background-color:#fff0f5;">`spack`</span><span
style="background-color:#fff0f5;">``  list tens` ``</span>, for example)
if you suspect that there might be a hyphen or you aren't certain on the
spelling. 

Just as information, most python packages in Spack begin with a \`py-\`
before the name that you may be most familiar with.

### <span id="Subheader: Spack Find">Spack Info</span>

The package that I have found has a name that is pretty close to the one
that I am expecting but I want to make CERTAIN it is the one I need. To
do this I can use the \`spack info\` command. The \`spack info\` command
will likely generate a lot to read. This will give you a package
description, its home URL, its Github URL, and variants and
dependencies. For now, I just want to make certain this is, in fact,
Tensorflow.


    [sw-slcolson@gpunode003 hpcadmins]$ spack info py-tensorflow

    Package:   py-tensorflow



    Description:

        TensorFlow is an open source machine learning framework for everyone.



    Homepage: https://www.tensorflow.org



    Preferred version:  

        2.14.0                 https://github.com/tensorflow/tensorflow/archive/v2.14.0.tar.gz

This is, in fact, the package that I am used to working with and wish to
use today. 

Now that I know the correct way to identify the package I want I can
check to see if it is installed on the TN Tech HPC using <span
style="background-color:#fff0f5;">`` ` ``</span><span
style="background-color:#fff0f5;">`spack`</span><span
style="background-color:#fff0f5;">``  find` ``</span> again:


    [sw-slcolson@gpunode003 hpcadmins]$ spack find py-tensorflow

    -- linux-rocky8-x86_64_v3 / gcc@8.5.0 ---------------------------

    py-tensorflow@2.8.4

    ==> 1 installed package

This is what I expected to see. At this point, you can proceed to the
[Spack Load](#Spack%20Load) section. 

If, however, you get a message like the one below, indicating that while
the package does exist, it is not available on the Tennessee Tech HPC,
complete the [HPC Spack Package
Request](https://services.tntech.edu/TDClient/1878/Portal/Requests/ServiceDet?ID=50539)
and we will be happy to work on getting it installed!


    [sw-slcolson@gpunode003 hpcadmins]$ spack find py-tensorflow 

    ==> No package matches the query: py-tensorflow

### <span id="Spack Load">Spack Load</span>

Now for the good part, how to load the package now that you have found
it. This is accomplished with a <span
style="background-color:#fff0f5;">`` ` ``</span><span
style="background-color:#fff0f5;">`spack`</span><span
style="background-color:#fff0f5;">``  load` ``</span> command.


    [sw-slcolson@gpunode003 hpcadmins]$ spack load py-tensorflow

 

## <span id="VersionsAndDependencies">Specifying Versions and Dependencies</span>

You can check for particular versions before loading them. The `@` sigil
is used to specify versions, both of packages and of compilers. For
instance, in searching for py-tensorflow I find that the HPC has several
versions and compilers available:


    [sw-slcolson@login ~]$ spack find py-tensorflow

    -- linux-rocky8-x86_64_v3 / gcc@8.5.0 ---------------------------

    py-tensorflow@2.8.4  py-tensorflow@2.8.4



    -- linux-rocky8-x86_64_v3 / gcc@9.5.0 ---------------------------

    py-tensorflow@2.10.1  py-tensorflow@2.11.1

    py-tensorflow@2.10.1  py-tensorflow@2.11.1

    ==> 6 installed packages

Adding the "-l" flag yields a slightly different view:


    [sw-slcolson@gpunode003 ~]$ spack find -l py-tensorflow

    -- linux-rocky8-x86_64_v3 / gcc@8.5.0 ---------------------------

    red52ck py-tensorflow@2.8.4  zu7ni7v py-tensorflow@2.8.4



    -- linux-rocky8-x86_64_v3 / gcc@9.5.0 ---------------------------

    xvruqqa py-tensorflow@2.10.1  ofjqf4j py-tensorflow@2.11.1

    5ypv26s py-tensorflow@2.10.1  nlbs3pp py-tensorflow@2.11.1

    ==> 6 installed packages

The seven digit codes that are listed before the package name and
version are called hashes. I know that I want to use
py-tensorflow@2.11.1 version but there are still two variants of it on
the HPC.  I can use the hashes to determine the differences between the
packages. 


    [sw-slcolson@gpunode003 ~]$ spack spec /ofjqf4j | head

    Input spec

    --------------------------------

    /ofjgf4j



    Concretized

    --------------------------------

    py-tensorflow@2.11.1%gcc@9.5.0~android~aws~computecpp+cuda+dynamic_kernels~gcp~gdr~hdfs~ignite~ios~jemalloc~kafka~mkl~monolithic~mpi~nccl~ngraph~numa~opencl~rocm~tensorrt~verbs+xla build_system=generic cuda_arch=37 patches=2017b3e arch=linux-rocky8-x86_64_v3


    [sw-slcolson@gpunode003 ~]$ spack spec /nlbs3pp | head

    Input spec

    --------------------------------

    /nlbs3pp



    Concretized

    --------------------------------

    py-tensorflow@2.11.1%gcc@9.5.0~android~aws~computecpp+cuda+dynamic_kernels~gcp~gdr~hdfs~ignite~ios~jemalloc~kafka~mkl~monolithic~mpi~nccl~ngraph~numa~opencl~rocm~tensorrt~verbs+xla build_system=generic cuda_arch=80 patches=2017b3e arch=linux-rocky8-x86_64_v3

From this I see that one package has cuda\_arch 80 and the other has
cuda\_arch 37. I want 80. I can load the package with the cuda\_arch
variant that I want with the following. 


    [sw-slcolson@gpunode003 ~]$ spack load py-tensorflow@2.11.1 cuda_arch=80

    [sw-slcolson@gpunode003 ~]$

By loading this package I have also loaded all of its dependencies. 


    [sw-slcolson@gpunode003 ~]$ spack find --loaded

    -- linux-rocky8-x86_64_v3 / gcc@8.5.0 ---------------------------

    autoconf@2.69        gmake@4.4.1           openblas@0.3.23               py-flit-core@3.7.1             py-pkgconfig@1.4.0                py-werkzeug@2.0.2

    automake@1.16.5      hdf5@1.14.1-2         openjdk@11.0.17_8             py-gast@0.5.3                  py-protobuf@3.17.3                py-wheel@0.37.1

    bazel@5.3.0          hwloc@2.9.1           openssl@1.1.1t                py-google-auth@2.16.2          py-pyasn1@0.4.8                   py-wrapt@1.14.1

    berkeley-db@18.1.40  libedit@3.1-20210216  pcre@8.45                     py-google-auth-oauthlib@0.4.6  py-pyasn1-modules@0.2.8           python@3.10.10

    binutils@2.40        libffi@3.4.4          perl@5.36.0                   py-google-pasta@0.2.0          py-requests@2.28.2                re2@2021-06-01

    bison@3.8.2          libgit2@1.6.4         perl-data-dumper@2.173        py-grpcio@1.52.0               py-requests-oauthlib@1.3.1        readline@8.2

    bzip2@1.0.8          libiconv@1.17         pkgconf@1.9.5                 py-h5py@3.8.0                  py-rsa@4.7.2                      rust@1.65.0

    c-ares@1.15.0        libssh2@1.10.0        protobuf@3.17.3               py-idna@3.3                    py-setuptools@63.4.3              swig@4.0.2-fortran

    cmake@3.26.3         libtool@2.4.7         py-absl-py@1.4.0              py-libclang@14.0.6             py-six@1.16.0                     texinfo@7.0.3

    cuda@11.4.4          libxml2@2.10.3        py-astunparse@1.6.3           py-markdown@3.4.1              py-tensorboard@2.11.2             xz@5.4.1

    cudnn@8.7.0.84-11.8  llvm@14.0.6           py-cachetools@5.2.0           py-numpy@1.24.3                py-tensorboard-data-server@0.6.1  zip@3.0

    curl@8.0.1           m4@1.4.19             py-certifi@2022.12.7          py-oauthlib@3.2.1              py-tensorboard-plugin-wit@1.8.1   zlib@1.2.13

    diffutils@3.9        ncurses@6.4           py-charset-normalizer@2.0.12  py-opt-einsum@3.3.0            py-termcolor@1.1.0                zstd@1.5.5

    gdbm@1.23            nghttp2@1.52.0        py-cython@0.29.33             py-packaging@23.0              py-typing-extensions@3.10.0.2

    gettext@0.21.1       ninja@1.11.1          py-flatbuffers@2.0.7          py-pip@23.0                    py-urllib3@1.26.12



    -- linux-rocky8-x86_64_v3 / gcc@9.5.0 ---------------------------

    py-tensorflow@2.11.1

    ==> 89 loaded packages

A spec may consist of the following pieces (for a full list of options
see the links listed in [What is Spack?](#WhatIsSpack)) :

-   Package name identifier (`zlib` above)

-   `@` Optional version specifier (`@1.2`)

-   `+` or `-` or `~` Optional variant specifiers (`+debug`, `-qt`,
    or `~qt`) for boolean variants. Use `++` or `--` or `~~` to
    propagate variants through the dependencies (`++debug`, `--qt`,
    or `~~qt`).

## <span id="Chaining">Chaining a User-managed Spack Installation From a Centrally-managed One</span>

Given a centrally-managed Spack 0.21.1 in `/opt/ohpc/pub/spack/v0.21.1`,
a user can leverage its packages and add their own packages
in `~/spack-0.21.1` as follows:

Download and extract Spack, then disable centrally-managed Spack:


    cd ~

    wget https://github.com/spack/spack/releases/download/v0.21.1/spack-0.21.1.tar.gz

    tar -zxf ~/spack-0.21.1.tar.gz

    echo 'export DISABLE_SYSTEM_SPACK=1' > ~/.spack_setup

Copy over some standard settings from the centrally-managed Spack:


    cp -a /opt/ohpc/pub/spack/v0.21.1/etc/spack/{linux,*.yaml} ~/spack-0.21.1/etc/spack/

Then, log out from the HPC completely to ensure the centrally-managed
Spack is disabled entirely, and log back in.

Verify the centrally-managed Spack is no longer used by default:


    [renfro@gpunode003(job 174321) ~]$ which spack

    /usr/bin/which: no spack in (/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/home/tntech.edu/renfro/.local/bin:/home/tntech.edu/renfro/bin)

Load the user-managed Spack and verify it has no packages installed:


    [renfro@gpunode003(job 174321) ~]$ . ~/spack-0.21.1/share/spack/setup-env.sh

    [renfro@gpunode003(job 174321) ~]$ spack find

    ==> 0 installed packages

Add a configuration file telling the user-managed Spack where the
centrally-managed Spack installation
is. `nano ~/spack-0.21.1/etc/spack/upstreams.yaml` and only use the
lines below:


    upstreams:

      tntech:

        install_tree: /opt/ohpc/pub/spack/v0.21.1/opt/spack

Install a simple package, notice that all of this package's dependencies
are already installed in the centrally-managed Spack, ensuring a much
faster installation process.


    [renfro@gpunode003(job 174321) ~]$ spack install cowsay

    [+] /opt/ohpc/pub/spack/v0.21.1/opt/spack/linux-rocky8-x86_64_v3/gcc-8.5.0/berkeley-db-18.1.40-hcm2ou2qqv7hksdgjx5s7wmoj577j3ri

    [+] /opt/ohpc/pub/spack/v0.21.1/opt/spack/linux-rocky8-x86_64_v3/gcc-8.5.0/bzip2-1.0.8-kqtusqz7a7tb6a4whcskjrc2dunjf3dr

    [+] /opt/ohpc/pub/spack/v0.21.1/opt/spack/linux-rocky8-x86_64_v3/gcc-8.5.0/ncurses-6.4-ilr5tjzk5pejy6kh25y7mczao23k3udj

    [+] /opt/ohpc/pub/spack/v0.21.1/opt/spack/linux-rocky8-x86_64_v3/gcc-8.5.0/zlib-1.2.13-s7zi7mma2xpws2mdh27j2qgnasg7uyb2

    [+] /opt/ohpc/pub/spack/v0.21.1/opt/spack/linux-rocky8-x86_64_v3/gcc-8.5.0/readline-8.2-b3k5lzac2mx2tdh7znkzpxofldi3z7rp

    [+] /opt/ohpc/pub/spack/v0.21.1/opt/spack/linux-rocky8-x86_64_v3/gcc-8.5.0/gdbm-1.23-rzxic7syszaantjc7mihxulc3eymh324

    [+] /opt/ohpc/pub/spack/v0.21.1/opt/spack/linux-rocky8-x86_64_v3/gcc-8.5.0/perl-5.36.0-im5hi7njqvu5jr3pocaq5pru3smqmb4r

    ==> Installing cowsay-3.04-jxz7d5p4iw5byfvba7f4e2nnenrdaxq2

    ==> No binary for cowsay-3.04-jxz7d5p4iw5byfvba7f4e2nnenrdaxq2 found: installing from source

    ==> Using cached archive: /home/tntech.edu/renfro/spack-0.21.1/var/spack/cache/_source-cache/archive/d8/d8b871332cfc1f0b6c16832ecca413ca0ac14d58626491a6733829e3d655878b.tar.gz

    ==> No patches needed for cowsay

    ==> cowsay: Executing phase: 'install'

    ==> cowsay: Successfully installed cowsay-3.04-jxz7d5p4iw5byfvba7f4e2nnenrdaxq2

      Stage: 0.03s.  Install: 0.15s.  Post-install: 0.12s.  Total: 0.46s

    [+] /home/tntech.edu/renfro/spack-0.21.1/opt/spack/linux-rocky8-x86_64_v3/gcc-8.5.0/cowsay-3.04-jxz7d5p4iw5byfvba7f4e2nnenrdaxq2

Verify where packages are installed. One is in the user-managed Spack
installation, the other is in the centrally-managed Spack installation:


    [renfro@gpunode003(job 174321) ~]$ spack find -p cowsay perl

    -- linux-rocky8-x86_64_v3 / gcc@8.5.0 ---------------------------

    cowsay@3.04  /home/tntech.edu/renfro/spack-0.21.1/opt/spack/linux-rocky8-x86_64_v3/gcc-8.5.0/cowsay-3.04-jxz7d5p4iw5byfvba7f4e2nnenrdaxq2

    perl@5.36.0  /opt/ohpc/pub/spack/v0.21.1/opt/spack/linux-rocky8-x86_64_v3/gcc-8.5.0/perl-5.36.0-im5hi7njqvu5jr3pocaq5pru3smqmb4r

    ==> 2 installed packages
