wayland_scanner_dep = dependency('wayland-scanner', native: true)
wayland_scanner_path = wayland_scanner_dep.get_variable(pkgconfig: 'wayland_scanner')
wayland_scanner = find_program(wayland_scanner_path, native: true)

protocols = [
	'frog-color-management-v1',
	'xx-color-management-v4',
	'color-management-v1',
]

protocols_client_src = []
protocols_server_src = []

foreach name : protocols
	code = custom_target(
		name + '-protocol.c',
		input: name + '.xml',
		output: '@BASENAME@-protocol.c',
		command: [wayland_scanner, 'private-code', '@INPUT@', '@OUTPUT@'],
	)

	server_header = custom_target(
		name + '-protocol.h',
		input: name + '.xml',
		output: '@BASENAME@-protocol.h',
		command: [wayland_scanner, 'server-header', '@INPUT@', '@OUTPUT@'],
	)

	client_header = custom_target(
		name + '-client-protocol.h',
		input: name + '.xml',
		output: '@BASENAME@-client-protocol.h',
		command: [wayland_scanner, 'client-header', '@INPUT@', '@OUTPUT@'],
	)

	protocols_server_src += [code, server_header]
	protocols_client_src += [code, client_header]
endforeach
