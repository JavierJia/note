# One line

read file into dict

    gps = dict(x.strip().split('\t',1) for x in open('gps.txt').readlines())

read file into set

    address = set(open('location.sort').read().split('\n'))


