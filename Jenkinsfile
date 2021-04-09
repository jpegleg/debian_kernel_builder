pipeline {
    agent {
        label 'deb'
    }


    stages {
        stage('Prep') {
            steps {
                sh "aptitude install libelf-dev libssl-dev linux-source fakeroot debhelper -y"
            }
            post {
                success {
                    sh "which make"
                    sh "which cc"
                    sh "which fakeroot"
                    sh "ls -larth /usr/src/linux*xz"
                }
            }
        }
        stage('Execute Build') {
            steps {
                sh "cd /srv/kbuild && cp /usr/src/linux-source-4.19.tar.xz ."
                sh "tar xvf linux-source-4.19.tar.xz && cd linux-source-4.19 && cp /boot/config-4.19.0-16-amd64 .config"
                sh "echo apply-deltas-here"
                sh "make deb-pkg LOCALVERSION=-customk KDEB_PKGVERSION=\$(make kernelversion)-1"
            }
            post {
                success {
                    sh "ls /srv/kbuild/linux*.deb"
                }
            }
        }
        stage('Publish and cleanup') {
            steps {
                sh "cp *.deb /srv/"
            }
            post {
                success {
                    sh "echo kernel_compile > /srv/kernel_compile.sums.txt"
                    sh "sha256sum /srv/linux-*deb >> /srv/kernel_compile.sums.txt"
                    sh "sha1sum /srv/linux-*deb >> /srv/kernel_compile.sums.txt"
                    sh "md5sum /srv/linux-*deb >> /srv/kernel_compile.sums.txt"
                }
            }
        }
    }
}
