project('com.github.sgpthomas.hourglass',
    'vala', 'c',
    version: '2.0.2',
    meson_version: '>=0.49.0'
)

gnome = import('gnome')
i18n = import('i18n')
add_project_arguments(
    '-DGETTEXT_PACKAGE="@0@"'.format(meson.project_name()),
    language:'c'
)

conf_data = configuration_data()
conf_data.set('EXEC_NAME', meson.project_name())
conf_data.set('DAEMON_EXEC_NAME', meson.project_name() + '-daemon')
conf_data.set_quoted('LOCALEDIR', get_option('prefix') / get_option('localedir'))
conf_data.set_quoted('GETTEXT_PACKAGE', meson.project_name())
config_file = configure_file(
    input: 'src' / 'Config.vala.in',
    output: 'Config.vala',
    configuration: conf_data
)

asresources = gnome.compile_resources(
    'as-resources',
    'data/' + meson.project_name() + '.gresource.xml',
    source_dir: 'data',
    c_name: 'as'
)

sources = files(
    'src' / 'Dialogs' / 'MultiSelectPopover.vala',
    'src' / 'Dialogs' / 'NewAlarmDialog.vala',
    'src' / 'Objects' / 'Counter.vala',
    'src' / 'Services' / 'DBusManager.vala',
    'src' / 'Views' / 'AbstractView.vala',
    'src' / 'Views' / 'AlarmView.vala',
    'src' / 'Views' / 'StopwatchView.vala',
    'src' / 'Views' / 'TimerView.vala',
    'src' / 'Widgets' / 'Alarm.vala',
    'src' / 'Widgets' / 'TimeSpinner.vala',
    'src' / 'Window' / 'MainWindow.vala',
    'src' / 'Hourglass.vala',
    'src' / 'Utils.vala'
)

executable(
    meson.project_name(),
    config_file,
    asresources,
    sources,
    dependencies: [
        dependency('gtk+-3.0', version: '>= 3.18'),
        dependency('gee-0.8'),
        dependency('granite', version: '>= 6.0.0'),
        dependency('libhandy-1')
    ],
    install: true,
)

install_data(
    'schemas' / meson.project_name() + '.gschema.xml',
    install_dir: get_option('datadir') / 'glib-2.0' / 'schemas'
)

subdir ('data')
subdir ('po')
subdir ('src' / 'Daemon')

meson.add_install_script('meson' / 'post_install.py')
